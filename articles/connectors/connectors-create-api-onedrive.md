---
title: "Соединитель OneDrive aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Обзор соединителя hello OneDrive с параметрами REST API"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="c4c54-103">Начало работы с соединителем OneDrive hello</span><span class="sxs-lookup"><span data-stu-id="c4c54-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="c4c54-104">Подключите tooOneDrive toomanage файлов, отправки, get, удалите файлы и многое другое.</span><span class="sxs-lookup"><span data-stu-id="c4c54-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="c4c54-105">С помощью OneDrive вы можете:</span><span class="sxs-lookup"><span data-stu-id="c4c54-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="c4c54-106">создавать рабочие процессы, сохраняя файлы в OneDrive, или обновлять имеющиеся файлы;</span><span class="sxs-lookup"><span data-stu-id="c4c54-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="c4c54-107">Используйте триггеры toostart рабочего процесса, если файл создается или обновляется в OneDrive.</span><span class="sxs-lookup"><span data-stu-id="c4c54-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="c4c54-108">Используйте действия toocreate файл, удалите файл и многое другое.</span><span class="sxs-lookup"><span data-stu-id="c4c54-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="c4c54-109">Например, после получения нового сообщения электронной почты Office 365 с вложением (триггер) может создаваться файл в OneDrive (действие).</span><span class="sxs-lookup"><span data-stu-id="c4c54-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="c4c54-110">В этом разделе показано, как toouse hello соединитель OneDrive в приложение логики, а также списки hello триггеров и действий.</span><span class="sxs-lookup"><span data-stu-id="c4c54-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="c4c54-111">toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c4c54-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="c4c54-112">Подключение tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="c4c54-112">Connect tooOneDrive</span></span>
<span data-ttu-id="c4c54-113">Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="c4c54-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="c4c54-114">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="c4c54-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="c4c54-115">Например, tooconnect tooOneDrive, необходимо сначала OneDrive *соединения*.</span><span class="sxs-lookup"><span data-stu-id="c4c54-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="c4c54-116">toocreate соединения, введите учетные данные hello, обычно используется служба hello tooaccess которых надо tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="c4c54-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="c4c54-117">Таким образом OneDrive, введите hello учетные данные tooyour OneDrive toocreate hello подключения к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c4c54-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="c4c54-118">Создайте соединение hello</span><span class="sxs-lookup"><span data-stu-id="c4c54-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="c4c54-119">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="c4c54-119">Use a trigger</span></span>
<span data-ttu-id="c4c54-120">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="c4c54-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="c4c54-121">Триггеры «опрос» hello службы в частоту и интервал.</span><span class="sxs-lookup"><span data-stu-id="c4c54-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="c4c54-122">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c4c54-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c4c54-123">В приложение логику hello введите «onedrive» tooget список триггеров hello:</span><span class="sxs-lookup"><span data-stu-id="c4c54-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="c4c54-124">Выберите триггер **When a file is modified** (При изменении файла).</span><span class="sxs-lookup"><span data-stu-id="c4c54-124">Select **When a file is modified**.</span></span> <span data-ttu-id="c4c54-125">Если подключение уже существует, выберите tooselect кнопку hello Показать выбора папки.</span><span class="sxs-lookup"><span data-stu-id="c4c54-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="c4c54-126">Если, запрашиваемые toosign в, а затем введите знак hello в соединении hello toocreate сведения.</span><span class="sxs-lookup"><span data-stu-id="c4c54-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="c4c54-127">[Создайте соединение hello](connectors-create-api-onedrive.md#create-the-connection) в этом разделе перечислены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c4c54-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c4c54-128">В этом примере логика приложения hello выполняется при создании файла в папке hello по выбору обновляется.</span><span class="sxs-lookup"><span data-stu-id="c4c54-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="c4c54-129">результаты hello toosee триггера, добавьте другое действие, которое отправляет вам сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c4c54-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="c4c54-130">Например, добавить hello Office 365 Outlook *отправить сообщение электронной почты* действие, которое сообщение электронной почты, при обновлении файла.</span><span class="sxs-lookup"><span data-stu-id="c4c54-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="c4c54-131">Выберите hello **изменить** кнопку и задайте hello **частоты** и **интервал** значения.</span><span class="sxs-lookup"><span data-stu-id="c4c54-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="c4c54-132">Например, если требуется toopoll триггер hello каждые 15 минут, задайте hello **частоты** слишком**минуту**и набор hello **интервал** слишком**15**.</span><span class="sxs-lookup"><span data-stu-id="c4c54-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="c4c54-133">**Сохранить** изменения (левом верхнем углу панели инструментов hello).</span><span class="sxs-lookup"><span data-stu-id="c4c54-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="c4c54-134">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="c4c54-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="c4c54-135">Использование действий</span><span class="sxs-lookup"><span data-stu-id="c4c54-135">Use an action</span></span>
<span data-ttu-id="c4c54-136">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="c4c54-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="c4c54-137">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c4c54-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c4c54-138">Выберите hello "плюс".</span><span class="sxs-lookup"><span data-stu-id="c4c54-138">Select hello plus sign.</span></span> <span data-ttu-id="c4c54-139">Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.</span><span class="sxs-lookup"><span data-stu-id="c4c54-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="c4c54-140">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="c4c54-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="c4c54-141">В текстовом поле hello введите «onedrive» tooget список всех доступных действий hello.</span><span class="sxs-lookup"><span data-stu-id="c4c54-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="c4c54-142">В этом примере для OneDrive мы выберем действие **Создать файл**.</span><span class="sxs-lookup"><span data-stu-id="c4c54-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="c4c54-143">Если подключение уже существует, то выберите hello **путь к папке** tooput hello, введите hello **имя файла**и выберите hello **содержимое файла** необходимо:</span><span class="sxs-lookup"><span data-stu-id="c4c54-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="c4c54-144">При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения.</span><span class="sxs-lookup"><span data-stu-id="c4c54-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="c4c54-145">[Создайте соединение hello](connectors-create-api-onedrive.md#create-the-connection) в этом разделе описываются эти свойства.</span><span class="sxs-lookup"><span data-stu-id="c4c54-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c4c54-146">В этом примере мы создадим файл в папке OneDrive.</span><span class="sxs-lookup"><span data-stu-id="c4c54-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="c4c54-147">Можно использовать результаты из другого файла OneDrive hello toocreate триггера.</span><span class="sxs-lookup"><span data-stu-id="c4c54-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="c4c54-148">Например, добавить hello Office 365 Outlook *при поступлении новой почты* триггера.</span><span class="sxs-lookup"><span data-stu-id="c4c54-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="c4c54-149">Затем добавьте hello OneDrive *создать файл* действие, которое использует hello вложений и Content-Type поля внутри ForEach toocreate hello новый файл в OneDrive.</span><span class="sxs-lookup"><span data-stu-id="c4c54-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="c4c54-150">**Сохранить** изменения (левом верхнем углу панели инструментов hello).</span><span class="sxs-lookup"><span data-stu-id="c4c54-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="c4c54-151">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="c4c54-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="c4c54-152">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c4c54-152">Connector-specific details</span></span>

<span data-ttu-id="c4c54-153">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="c4c54-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c4c54-154">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c4c54-154">More connectors</span></span>
<span data-ttu-id="c4c54-155">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c4c54-155">Go back toohello [APIs list](apis-list.md).</span></span>
