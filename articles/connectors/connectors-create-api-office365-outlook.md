---
title: "Добавление соединителя Office 365 Outlook в приложения логики | Документация Майкрософт"
description: "Сведения о создании приложений логики с использованием соединителя Office 365 для взаимодействия с этой службой. Например, он позволяет создавать, редактировать и обновлять контакты и элементы календаря."
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
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="c2caa-104">Начало работы с соединителем Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="c2caa-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="c2caa-105">Соединитель Office 365 Outlook обеспечивает взаимодействие с Outlook в Office 365.</span><span class="sxs-lookup"><span data-stu-id="c2caa-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="c2caa-106">С помощью этого соединителя можно создавать, изменять и обновлять контакты и элементы календаря, а также обмениваться сообщениями электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c2caa-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="c2caa-107">Office 365 Outlook позволяет следующее:</span><span class="sxs-lookup"><span data-stu-id="c2caa-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="c2caa-108">создать рабочий процесс с использованием возможностей электронной почты и календаря в Office 365;</span><span class="sxs-lookup"><span data-stu-id="c2caa-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="c2caa-109">использовать триггеры для запуска рабочего процесса при получении сообщения электронной почты, обновлении элемента календаря и т. д.;</span><span class="sxs-lookup"><span data-stu-id="c2caa-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="c2caa-110">использовать действия для отправки сообщения электронной почты, создания события календаря и т. д.</span><span class="sxs-lookup"><span data-stu-id="c2caa-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="c2caa-111">Например, при создании объекта в Salesforce (триггер) будет отправляться сообщение электронной почты в Office 365 Outlook (действие).</span><span class="sxs-lookup"><span data-stu-id="c2caa-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="c2caa-112">В этой статье содержатся сведения об использовании соединителя Office 365 Outlook в приложении логики, а также перечислены предоставляемые им триггеры и действия.</span><span class="sxs-lookup"><span data-stu-id="c2caa-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="c2caa-113">Эта версия статьи предназначена для общедоступного выпуска приложений логики.</span><span class="sxs-lookup"><span data-stu-id="c2caa-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="c2caa-114">Дополнительные сведения о приложениях логики см. в статье, посвященной [приложениям логики](../logic-apps/logic-apps-what-are-logic-apps.md), и [руководстве по созданию приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c2caa-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="c2caa-115">Подключение к Office 365</span><span class="sxs-lookup"><span data-stu-id="c2caa-115">Connect to Office 365</span></span>
<span data-ttu-id="c2caa-116">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="c2caa-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="c2caa-117">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="c2caa-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="c2caa-118">Например, чтобы подключиться к Office 365 Outlook, сначала необходимо установить *подключение* к службе Office 365.</span><span class="sxs-lookup"><span data-stu-id="c2caa-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="c2caa-119">Чтобы создать подключение, введите учетные данные, которые используются для доступа к определенной службе.</span><span class="sxs-lookup"><span data-stu-id="c2caa-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="c2caa-120">Для создания подключения к Office 365 Outlook необходимо использовать учетные данные учетной записи Office 365.</span><span class="sxs-lookup"><span data-stu-id="c2caa-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="c2caa-121">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="c2caa-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="c2caa-122">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="c2caa-122">Use a trigger</span></span>
<span data-ttu-id="c2caa-123">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="c2caa-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c2caa-124">Триггеры опрашивают службу с определенным интервалом и частотой.</span><span class="sxs-lookup"><span data-stu-id="c2caa-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="c2caa-125">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c2caa-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c2caa-126">Чтобы открыть список триггеров, в текстовом поле приложения логики введите office 365.</span><span class="sxs-lookup"><span data-stu-id="c2caa-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="c2caa-127">Выберите триггер Office 365 Outlook **When an upcoming event is starting soon** (Если приближается время начала предстоящего события).</span><span class="sxs-lookup"><span data-stu-id="c2caa-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="c2caa-128">Если подключение уже существует, выберите календарь в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="c2caa-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="c2caa-129">Если появится запрос на вход, введите учетные данные для входа, чтобы создать подключение.</span><span class="sxs-lookup"><span data-stu-id="c2caa-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="c2caa-130">Дополнительные сведения о создании подключения см. в [разделе выше](connectors-create-api-office365-outlook.md#create-the-connection).</span><span class="sxs-lookup"><span data-stu-id="c2caa-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c2caa-131">В этом примере приложение логики выполняется при обновлении события календаря.</span><span class="sxs-lookup"><span data-stu-id="c2caa-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="c2caa-132">Чтобы увидеть результаты работы триггера, добавьте другое действие, которое отправляет текстовое сообщение.</span><span class="sxs-lookup"><span data-stu-id="c2caa-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="c2caa-133">Например, добавьте действие Twilio *Send message* (Отправить сообщение), которое отправляет текстовое сообщение, если событие календаря должно запуститься через 15 минут.</span><span class="sxs-lookup"><span data-stu-id="c2caa-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="c2caa-134">Нажмите кнопку **Изменить** и задайте **частоту** и **интервал**.</span><span class="sxs-lookup"><span data-stu-id="c2caa-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="c2caa-135">Например, если требуется, чтобы триггер выполнял опрос каждые 15 минут, задайте для параметра **Частота** значение **Минута**, а для параметра **Интервал** — **15**.</span><span class="sxs-lookup"><span data-stu-id="c2caa-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="c2caa-136">**Сохраните** изменения, нажав соответствующую кнопку в левом верхнем углу панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="c2caa-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="c2caa-137">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="c2caa-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="c2caa-138">Использование действий</span><span class="sxs-lookup"><span data-stu-id="c2caa-138">Use an action</span></span>
<span data-ttu-id="c2caa-139">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="c2caa-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c2caa-140">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c2caa-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c2caa-141">Щелкните знак "плюс".</span><span class="sxs-lookup"><span data-stu-id="c2caa-141">Select the plus sign.</span></span> <span data-ttu-id="c2caa-142">Отобразятся следующие команды: **Добавить действие**, **Добавить условие** или **Еще**.</span><span class="sxs-lookup"><span data-stu-id="c2caa-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="c2caa-143">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="c2caa-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="c2caa-144">Чтобы открыть список всех доступных действий, в текстовом поле введите office 365.</span><span class="sxs-lookup"><span data-stu-id="c2caa-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="c2caa-145">В этом примере мы выберем действие Office 365 Outlook **Создание контакта**.</span><span class="sxs-lookup"><span data-stu-id="c2caa-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="c2caa-146">Если подключение уже существует, задайте **идентификатор папки**, **имя** и другие свойства:</span><span class="sxs-lookup"><span data-stu-id="c2caa-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="c2caa-147">Если появится запрос на предоставление сведений о подключении, введите их, чтобы создать подключение.</span><span class="sxs-lookup"><span data-stu-id="c2caa-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="c2caa-148">Эти свойства описаны в разделе о [создании подключения](connectors-create-api-office365-outlook.md#create-the-connection) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c2caa-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c2caa-149">В этом примере мы создадим контакт в Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="c2caa-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="c2caa-150">Чтобы создать контакт, можно использовать выходные данные другого триггера.</span><span class="sxs-lookup"><span data-stu-id="c2caa-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="c2caa-151">Например, добавьте триггер SalesForce *При создании объекта*.</span><span class="sxs-lookup"><span data-stu-id="c2caa-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="c2caa-152">Затем добавьте действие Office 365 Outlook *Создание контакта*, которое создает контакт в Office 365, используя значения в полях SalesForce.</span><span class="sxs-lookup"><span data-stu-id="c2caa-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="c2caa-153">**Сохраните** изменения, нажав соответствующую кнопку в левом верхнем углу панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="c2caa-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="c2caa-154">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="c2caa-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="c2caa-155">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c2caa-155">Connector-specific details</span></span>

<span data-ttu-id="c2caa-156">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="c2caa-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c2caa-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2caa-157">Next Steps</span></span>
<span data-ttu-id="c2caa-158">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c2caa-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="c2caa-159">Чтобы узнать, какие еще соединители доступны в Logic Apps, просмотрите [список интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c2caa-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

