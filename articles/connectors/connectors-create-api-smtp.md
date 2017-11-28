---
title: "Соединитель SMTP в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Подключение к SMTP для отправки электронной почты."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="2bc2c-104">Начало работы с соединителем SMTP</span><span class="sxs-lookup"><span data-stu-id="2bc2c-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="2bc2c-105">Подключение к SMTP для отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="2bc2c-106">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="2bc2c-107">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2bc2c-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="2bc2c-108">Подключение к SMTP</span><span class="sxs-lookup"><span data-stu-id="2bc2c-108">Connect to SMTP</span></span>
<span data-ttu-id="2bc2c-109">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="2bc2c-110">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="2bc2c-111">Например, чтобы подключиться к SMTP, сначала необходимо создать *подключение* по протоколу SMTP.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="2bc2c-112">Чтобы создать подключение, введите учетные данные, которые используются для доступа к определенной службе.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="2bc2c-113">Таким образом, чтобы создать подключение по протоколу SMTP, следует ввести имя подключения, адрес SMTP-сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="2bc2c-114">Создание подключения к SMTP</span><span class="sxs-lookup"><span data-stu-id="2bc2c-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="2bc2c-115">Использование триггера SMTP</span><span class="sxs-lookup"><span data-stu-id="2bc2c-115">Use an SMTP trigger</span></span>
<span data-ttu-id="2bc2c-116">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="2bc2c-117">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="2bc2c-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="2bc2c-118">Так как SMTP не предоставляет триггеры, мы используем триггер **Salesforce - When an object is created** (Salesforce — при создании объекта).</span><span class="sxs-lookup"><span data-stu-id="2bc2c-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="2bc2c-119">Этот триггер активируется при создании объекта в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="2bc2c-120">В нашем примере мы настроим триггер таким образом, чтобы при каждом создании интереса в Salesforce выполнялось действие *Send Email* через соединитель SMTP. При этом будет отправляться уведомление об этом интересе.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="2bc2c-121">В конструкторе приложений логики в поле поиска введите запрос *salesforce* , а затем выберите триггер **Salesforce — при создании объекта** .</span><span class="sxs-lookup"><span data-stu-id="2bc2c-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="2bc2c-122">Отобразится элемент управления **При создании объекта** .</span><span class="sxs-lookup"><span data-stu-id="2bc2c-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="2bc2c-123">Укажите **тип объекта** , а затем выберите *Интерес* из списка объектов.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="2bc2c-124">На этом шаге вы указываете, что создаете триггер, который будет уведомлять приложение логики о создании интереса в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="2bc2c-125">Ваш триггер создан.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="2bc2c-126">Использование действия SMTP</span><span class="sxs-lookup"><span data-stu-id="2bc2c-126">Use an SMTP action</span></span>
<span data-ttu-id="2bc2c-127">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="2bc2c-128">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="2bc2c-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="2bc2c-129">Теперь, когда триггер добавлен, выполните следующие действия, чтобы добавить действие SMTP, которое будет выполняться при создании интереса в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="2bc2c-130">Нажмите кнопку **+ Новый шаг**, чтобы добавить действие, которое будет выполняться после создания интереса.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="2bc2c-131">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-131">Select **Add an action**.</span></span> <span data-ttu-id="2bc2c-132">Откроется поле поиска. В этом поле вы можете выполнить поиск действия, которое нужно применить.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="2bc2c-133">Введите *smtp* в поле поиска, чтобы найти действия, связанные с SMTP.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="2bc2c-134">Выберите **SMTP - Send Email** (SMTP — отправка электронного сообщения) в качестве действия, которое следует выполнять при создании интереса.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="2bc2c-135">Откроется блок управления действием.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-135">The action control block opens.</span></span> <span data-ttu-id="2bc2c-136">Установите подключение SMTP в блоке конструктора, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="2bc2c-137">В блоке **SMTP - Send Email** (SMTP — отправка электронного сообщения) введите необходимые сведения об электронной почте.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="2bc2c-138">Сохраните данные, чтобы активировать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="2bc2c-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="2bc2c-139">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="2bc2c-139">Connector-specific details</span></span>

<span data-ttu-id="2bc2c-140">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="2bc2c-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2bc2c-141">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="2bc2c-141">More connectors</span></span>
<span data-ttu-id="2bc2c-142">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2bc2c-142">Go back to the [APIs list](apis-list.md).</span></span>