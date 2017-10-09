---
title: "Соединитель aaaSMTP в приложения логики Azure | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите tooSMTP toosend по электронной почте."
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
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="c07d6-104">Приступая к работе с hello соединитель SMTP</span><span class="sxs-lookup"><span data-stu-id="c07d6-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="c07d6-105">Подключите tooSMTP toosend по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="c07d6-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="c07d6-106">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="c07d6-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="c07d6-107">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c07d6-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="c07d6-108">Подключение tooSMTP</span><span class="sxs-lookup"><span data-stu-id="c07d6-108">Connect tooSMTP</span></span>
<span data-ttu-id="c07d6-109">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="c07d6-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="c07d6-110">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="c07d6-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="c07d6-111">Например, tooconnect tooSMTP, необходимо сначала SMTP *соединения*.</span><span class="sxs-lookup"><span data-stu-id="c07d6-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="c07d6-112">toocreate соединения, введите учетные данные hello, обычно используется tooaccess hello службы при подключении.</span><span class="sxs-lookup"><span data-stu-id="c07d6-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="c07d6-113">Таким образом в примере hello SMTP введите имя подключения tooyour hello учетные данные, адреса SMTP-сервера и подключение пользователя входа сведения toocreate hello tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="c07d6-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="c07d6-114">Создание tooSMTP подключения</span><span class="sxs-lookup"><span data-stu-id="c07d6-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="c07d6-115">Использование триггера SMTP</span><span class="sxs-lookup"><span data-stu-id="c07d6-115">Use an SMTP trigger</span></span>
<span data-ttu-id="c07d6-116">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="c07d6-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="c07d6-117">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c07d6-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="c07d6-118">В этом примере, поскольку SMTP не имеет триггер свои собственные, мы будем использовать hello **Salesforce - при создании объекта** триггера.</span><span class="sxs-lookup"><span data-stu-id="c07d6-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="c07d6-119">Этот триггер активируется при создании объекта в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c07d6-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="c07d6-120">В нашем примере мы составим его таким образом, что каждый раз создается новый интерес в Salesforce, *письмо* действие выполняется с помощью соединителя hello SMTP уведомление создается новый интерес hello.</span><span class="sxs-lookup"><span data-stu-id="c07d6-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="c07d6-121">Введите *salesforce* в поле поиска hello в конструкторе приложений логики hello выберите hello **Salesforce - при создании объекта** триггера.</span><span class="sxs-lookup"><span data-stu-id="c07d6-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="c07d6-122">Hello **при создании объекта** отображается элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c07d6-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="c07d6-123">Выберите hello **тип объекта** выберите *привести* hello списке объектов.</span><span class="sxs-lookup"><span data-stu-id="c07d6-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="c07d6-124">На этом шаге вы указываете, что создаете триггер, который будет уведомлять приложение логики о создании интереса в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c07d6-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="c07d6-125">был создан триггер Hello.</span><span class="sxs-lookup"><span data-stu-id="c07d6-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="c07d6-126">Использование действия SMTP</span><span class="sxs-lookup"><span data-stu-id="c07d6-126">Use an SMTP action</span></span>
<span data-ttu-id="c07d6-127">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="c07d6-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="c07d6-128">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c07d6-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="c07d6-129">Теперь, когда hello триггер был добавлен, выполните эти шаги tooadd SMTP действие, которое будет выполняться при создании нового интереса в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c07d6-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="c07d6-130">Выберите **+ новый шаг** действие hello tooadd хотелось бы tootake при создании нового интереса.</span><span class="sxs-lookup"><span data-stu-id="c07d6-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="c07d6-131">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="c07d6-131">Select **Add an action**.</span></span> <span data-ttu-id="c07d6-132">Открывает окна поиска hello поиска для любого действия вы хотели бы tootake.</span><span class="sxs-lookup"><span data-stu-id="c07d6-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="c07d6-133">Введите *smtp* toosearch для tooSMTP связанные действия.</span><span class="sxs-lookup"><span data-stu-id="c07d6-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="c07d6-134">Выберите **SMTP - Отправка сообщения** как hello tootake действие, когда создается новый интерес hello.</span><span class="sxs-lookup"><span data-stu-id="c07d6-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="c07d6-135">Открывает блок управления действие Hello.</span><span class="sxs-lookup"><span data-stu-id="c07d6-135">hello action control block opens.</span></span> <span data-ttu-id="c07d6-136">Если вы еще не сделали это будет иметь tooestablish подключения к smtp в блоке конструктора hello.</span><span class="sxs-lookup"><span data-stu-id="c07d6-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="c07d6-137">Входные данные требуемой электронной почты в hello **SMTP - Отправка сообщения** блока.</span><span class="sxs-lookup"><span data-stu-id="c07d6-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="c07d6-138">Сохраните изменения в порядке tooactivate рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="c07d6-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="c07d6-139">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c07d6-139">Connector-specific details</span></span>

<span data-ttu-id="c07d6-140">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="c07d6-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c07d6-141">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="c07d6-141">More connectors</span></span>
<span data-ttu-id="c07d6-142">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c07d6-142">Go back toohello [APIs list](apis-list.md).</span></span>
