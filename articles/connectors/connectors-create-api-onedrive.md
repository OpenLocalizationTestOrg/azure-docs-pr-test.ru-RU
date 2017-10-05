---
title: "Добавление соединителя OneDrive в приложения логики | Документация Майкрософт"
description: "Обзор соединителя OneDrive с параметрами интерфейса API REST"
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
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="e2d70-103">Начало работы с соединителем OneDrive</span><span class="sxs-lookup"><span data-stu-id="e2d70-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="e2d70-104">Подключитесь к OneDrive для управления файлами, включая передачу, получение, удаление файлов и многое другое.</span><span class="sxs-lookup"><span data-stu-id="e2d70-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="e2d70-105">С помощью OneDrive вы можете:</span><span class="sxs-lookup"><span data-stu-id="e2d70-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="e2d70-106">создавать рабочие процессы, сохраняя файлы в OneDrive, или обновлять имеющиеся файлы;</span><span class="sxs-lookup"><span data-stu-id="e2d70-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="e2d70-107">использовать триггеры для запуска рабочего процесса при создании или обновлении файлов в OneDrive;</span><span class="sxs-lookup"><span data-stu-id="e2d70-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="e2d70-108">использовать действия по созданию, удалению файлов и т. д.</span><span class="sxs-lookup"><span data-stu-id="e2d70-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="e2d70-109">Например, после получения нового сообщения электронной почты Office 365 с вложением (триггер) может создаваться файл в OneDrive (действие).</span><span class="sxs-lookup"><span data-stu-id="e2d70-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="e2d70-110">В этой статье содержатся сведения об использовании соединителя OneDrive в приложении логики, а также перечислены предоставляемые им триггеры и действия.</span><span class="sxs-lookup"><span data-stu-id="e2d70-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="e2d70-111">Дополнительные сведения о приложениях логики см. в статье, посвященной [приложениям логики](../logic-apps/logic-apps-what-are-logic-apps.md), и [руководстве по созданию приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e2d70-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="e2d70-112">Создание подключения к OneDrive</span><span class="sxs-lookup"><span data-stu-id="e2d70-112">Connect to OneDrive</span></span>
<span data-ttu-id="e2d70-113">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="e2d70-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="e2d70-114">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="e2d70-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e2d70-115">Например, чтобы подключиться к OneDrive, сначала необходимо создать соответствующее *подключение*.</span><span class="sxs-lookup"><span data-stu-id="e2d70-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="e2d70-116">Чтобы создать подключение, введите учетные данные, которые используются для доступа к определенной службе.</span><span class="sxs-lookup"><span data-stu-id="e2d70-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="e2d70-117">Для создания подключения к OneDrive необходимо использовать учетные данные учетной записи OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e2d70-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="e2d70-118">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="e2d70-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="e2d70-119">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="e2d70-119">Use a trigger</span></span>
<span data-ttu-id="e2d70-120">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="e2d70-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="e2d70-121">Триггеры опрашивают службу с определенным интервалом и частотой.</span><span class="sxs-lookup"><span data-stu-id="e2d70-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="e2d70-122">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e2d70-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e2d70-123">Чтобы открыть список триггеров, в текстовом поле приложения логики введите onedrive.</span><span class="sxs-lookup"><span data-stu-id="e2d70-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="e2d70-124">Выберите триггер **When a file is modified** (При изменении файла).</span><span class="sxs-lookup"><span data-stu-id="e2d70-124">Select **When a file is modified**.</span></span> <span data-ttu-id="e2d70-125">Если подключение уже существует, нажмите кнопку "Выбрать", чтобы указать папку.</span><span class="sxs-lookup"><span data-stu-id="e2d70-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="e2d70-126">Если появится запрос на вход, введите учетные данные для входа, чтобы создать подключение.</span><span class="sxs-lookup"><span data-stu-id="e2d70-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="e2d70-127">Дополнительные сведения о [создании подключения](connectors-create-api-onedrive.md#create-the-connection) см. в разделе выше.</span><span class="sxs-lookup"><span data-stu-id="e2d70-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e2d70-128">В этом примере приложение логики запускается при обновлении файла в выбранной папке.</span><span class="sxs-lookup"><span data-stu-id="e2d70-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="e2d70-129">Чтобы увидеть результаты триггера, добавьте другое действие, которое отправляет сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="e2d70-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="e2d70-130">Например, добавьте действие Office 365 Outlook *Отправить сообщение электронной почты* для отправки вам сообщения электронной почты после обновления файла.</span><span class="sxs-lookup"><span data-stu-id="e2d70-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="e2d70-131">Нажмите кнопку **Изменить** и задайте **частоту** и **интервал**.</span><span class="sxs-lookup"><span data-stu-id="e2d70-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="e2d70-132">Например, если требуется, чтобы триггер выполнял опрос каждые 15 минут, задайте для параметра **Частота** значение **Минута**, а для параметра **Интервал** — **15**.</span><span class="sxs-lookup"><span data-stu-id="e2d70-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="e2d70-133">**Сохраните** изменения, нажав соответствующую кнопку в левом верхнем углу панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="e2d70-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="e2d70-134">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="e2d70-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="e2d70-135">Использование действий</span><span class="sxs-lookup"><span data-stu-id="e2d70-135">Use an action</span></span>
<span data-ttu-id="e2d70-136">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="e2d70-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="e2d70-137">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e2d70-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="e2d70-138">Щелкните знак "плюс".</span><span class="sxs-lookup"><span data-stu-id="e2d70-138">Select the plus sign.</span></span> <span data-ttu-id="e2d70-139">Отобразятся следующие команды: **Добавить действие**, **Добавить условие** или **Еще**.</span><span class="sxs-lookup"><span data-stu-id="e2d70-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="e2d70-140">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="e2d70-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e2d70-141">Чтобы открыть список всех доступных действий, в текстовом поле введите onedrive.</span><span class="sxs-lookup"><span data-stu-id="e2d70-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="e2d70-142">В этом примере для OneDrive мы выберем действие **Создать файл**.</span><span class="sxs-lookup"><span data-stu-id="e2d70-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="e2d70-143">Если подключение уже существует, укажите **путь к папке**, в которую необходимо поместить файл, введите **имя файла** и выберите тип **содержимого файла**.</span><span class="sxs-lookup"><span data-stu-id="e2d70-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="e2d70-144">Если появится запрос на предоставление сведений о подключении, введите их, чтобы создать подключение.</span><span class="sxs-lookup"><span data-stu-id="e2d70-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="e2d70-145">Эти свойства описаны в разделе о [создании подключения](connectors-create-api-onedrive.md#create-the-connection) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e2d70-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e2d70-146">В этом примере мы создадим файл в папке OneDrive.</span><span class="sxs-lookup"><span data-stu-id="e2d70-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="e2d70-147">Чтобы создать файл OneDrive, можно использовать выходные данные другого триггера.</span><span class="sxs-lookup"><span data-stu-id="e2d70-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="e2d70-148">Например, добавьте триггер Office 365 Outlook *When a new email arrives* (При получении новой почты).</span><span class="sxs-lookup"><span data-stu-id="e2d70-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="e2d70-149">Затем, чтобы создать файл в OneDrive, добавьте действие OneDrive *Создать файл*, для которого заданы поля "Вложения" и "Тип содержимого" в ForEach.</span><span class="sxs-lookup"><span data-stu-id="e2d70-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="e2d70-150">**Сохраните** изменения, нажав соответствующую кнопку в левом верхнем углу панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="e2d70-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="e2d70-151">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="e2d70-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="e2d70-152">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="e2d70-152">Connector-specific details</span></span>

<span data-ttu-id="e2d70-153">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="e2d70-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e2d70-154">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="e2d70-154">More connectors</span></span>
<span data-ttu-id="e2d70-155">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e2d70-155">Go back to the [APIs list](apis-list.md).</span></span>