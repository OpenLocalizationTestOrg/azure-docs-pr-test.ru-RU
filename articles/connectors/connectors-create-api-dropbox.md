---
title: "Соединитель Dropbox в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Подключитесь к Dropbox, чтобы управлять файлами. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов в Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="191fe-105">Начало работы с соединителем Dropbox</span><span class="sxs-lookup"><span data-stu-id="191fe-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="191fe-106">Подключитесь к Dropbox, чтобы управлять файлами.</span><span class="sxs-lookup"><span data-stu-id="191fe-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="191fe-107">Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов в Dropbox.</span><span class="sxs-lookup"><span data-stu-id="191fe-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="191fe-108">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="191fe-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="191fe-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="191fe-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="191fe-110">Подключение к Dropbox</span><span class="sxs-lookup"><span data-stu-id="191fe-110">Connect to Dropbox</span></span>
<span data-ttu-id="191fe-111">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="191fe-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="191fe-112">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="191fe-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="191fe-113">Например, чтобы подключиться к Dropbox, сначала необходимо создать *подключение* к Dropbox.</span><span class="sxs-lookup"><span data-stu-id="191fe-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="191fe-114">Чтобы создать подключение, необходимо ввести учетные данные, которые обычно используются для доступа к определенной службе.</span><span class="sxs-lookup"><span data-stu-id="191fe-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="191fe-115">То есть для создания подключения к Dropbox вам понадобятся учетные данные учетной записи Dropbox.</span><span class="sxs-lookup"><span data-stu-id="191fe-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> <span data-ttu-id="191fe-116">Дополнительные сведения о подключениях см. [здесь]().</span><span class="sxs-lookup"><span data-stu-id="191fe-116">[Learn more about connections]()</span></span>

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="191fe-117">Создание подключения к Dropbox</span><span class="sxs-lookup"><span data-stu-id="191fe-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="191fe-118">Использование триггера Dropbox</span><span class="sxs-lookup"><span data-stu-id="191fe-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="191fe-119">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="191fe-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="191fe-120">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="191fe-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="191fe-121">В этом примере мы будем использовать триггер **When a file is created** (При создании файла).</span><span class="sxs-lookup"><span data-stu-id="191fe-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="191fe-122">Когда этот триггер активируется, мы вызовем действие Dropbox **Get file content using path** (Получение содержимого файла с помощью пути).</span><span class="sxs-lookup"><span data-stu-id="191fe-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="191fe-123">Введите запрос *dropbox* в поле поиска в конструкторе Logic Apps, а затем выберите триггер **Dropbox - When a file is created** (Dropbox — при создании файла).</span><span class="sxs-lookup"><span data-stu-id="191fe-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="191fe-124">Выберите папку для отслеживания создания файла.</span><span class="sxs-lookup"><span data-stu-id="191fe-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="191fe-125">Щелкните многоточие "…" (на снимке экрана выделено красной рамкой) и перейдите к папке, которую вы хотите выбрать в качестве входных данных триггера.</span><span class="sxs-lookup"><span data-stu-id="191fe-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="191fe-126">Использование действия Dropbox</span><span class="sxs-lookup"><span data-stu-id="191fe-126">Use a Dropbox action</span></span>
<span data-ttu-id="191fe-127">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="191fe-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="191fe-128">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="191fe-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="191fe-129">Теперь, когда триггер добавлен, выполните следующие действия, чтобы добавить действие, которое получит новое содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="191fe-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="191fe-130">Нажмите кнопку **+ Новый шаг**, чтобы добавить действие, которое будет выполняться после создания нового файла.</span><span class="sxs-lookup"><span data-stu-id="191fe-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="191fe-131">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="191fe-131">Select **Add an action**.</span></span> <span data-ttu-id="191fe-132">Откроется поле поиска. В этом поле вы можете выполнить поиск действия, которое нужно применить.</span><span class="sxs-lookup"><span data-stu-id="191fe-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="191fe-133">Введите запрос *dropbox*, чтобы найти действия, связанные с Dropbox.</span><span class="sxs-lookup"><span data-stu-id="191fe-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="191fe-134">Выберите **Dropbox - Get file content using path** (Dropbox — получение содержимого файла с помощью пути) в качестве действия, которое будет выполняться после создания файла в выбранной папке Dropbox.</span><span class="sxs-lookup"><span data-stu-id="191fe-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="191fe-135">Откроется блок управления действием.</span><span class="sxs-lookup"><span data-stu-id="191fe-135">The action control block opens.</span></span> <span data-ttu-id="191fe-136">Вам будет предложено авторизовать приложение логики для доступа к учетной записи Dropbox, если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="191fe-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="191fe-137">Щелкните многоточие "…" (находится в правой части элемента управления **Путь к файлу**) и перейдите к файлу, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="191fe-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="191fe-138">Или используйте маркер **file path**, чтобы ускорить создание приложения логики.</span><span class="sxs-lookup"><span data-stu-id="191fe-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="191fe-139">Сохраните изменения и создайте новый файл в Dropbox, чтобы активировать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="191fe-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="191fe-140">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="191fe-140">Connector-specific details</span></span>

<span data-ttu-id="191fe-141">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="191fe-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="191fe-142">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="191fe-142">More connectors</span></span>
<span data-ttu-id="191fe-143">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="191fe-143">Go back to the [APIs list](apis-list.md).</span></span>