---
title: "aaaLearn как toouse hello соединителя Twitter в приложениях для логики | Документы Microsoft"
description: "Обзор соединителя Twitter с параметрами REST API"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="eb3ef-103">Начало работы с соединителем hello Twitter</span><span class="sxs-lookup"><span data-stu-id="eb3ef-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="eb3ef-104">С помощью соединителя Twitter hello можно:</span><span class="sxs-lookup"><span data-stu-id="eb3ef-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="eb3ef-105">публиковать и получать твиты;</span><span class="sxs-lookup"><span data-stu-id="eb3ef-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="eb3ef-106">получать доступ к временным шкалам, просматривать друзей и подписчиков;</span><span class="sxs-lookup"><span data-stu-id="eb3ef-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="eb3ef-107">Выполните любое из hello других действий и триггеров, описанные ниже</span><span class="sxs-lookup"><span data-stu-id="eb3ef-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="eb3ef-108">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="eb3ef-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="eb3ef-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="eb3ef-110">Подключение tooTwitter</span><span class="sxs-lookup"><span data-stu-id="eb3ef-110">Connect tooTwitter</span></span>
<span data-ttu-id="eb3ef-111">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="eb3ef-112">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="eb3ef-113">Создание tooTwitter подключения</span><span class="sxs-lookup"><span data-stu-id="eb3ef-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="eb3ef-114">Использование триггера Twitter</span><span class="sxs-lookup"><span data-stu-id="eb3ef-114">Use a Twitter trigger</span></span>
<span data-ttu-id="eb3ef-115">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="eb3ef-116">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="eb3ef-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="eb3ef-117">В этом примере будет показано как toouse hello **при учете новый твит** инициирует toosearch для #Seattle и, при обнаружении #Seattle обновления файла в общий банк данных с текстом hello твит hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="eb3ef-118">В примере enterprise может поиск hello название вашей компании и обновления базы данных SQL с текстом hello твит hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="eb3ef-119">Введите *twitter* в поле поиска hello в конструкторе приложений логики hello выберите hello **Twitter - при публикации новых твит** триггера</span><span class="sxs-lookup"><span data-stu-id="eb3ef-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="eb3ef-120">![Изображение 1. Триггер Twitter](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="eb3ef-121">Введите *#Seattle* в hello **искомый текст** управления</span><span class="sxs-lookup"><span data-stu-id="eb3ef-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="eb3ef-122">![Изображение 2. Триггер Twitter](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="eb3ef-123">На этом этапе приложение логики, были настроены триггер начала запуска hello других триггеров и действий в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb3ef-124">Логика приложения toobe функциональной должен содержать хотя бы один триггер и одно действие.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="eb3ef-125">Следуйте указаниям hello hello Далее раздел tooadd действие.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="eb3ef-126">Добавить условие</span><span class="sxs-lookup"><span data-stu-id="eb3ef-126">Add a condition</span></span>
<span data-ttu-id="eb3ef-127">Так как нас интересуют только твиты у пользователей с более чем 50 пользователей, условие, которое подтверждает hello число последователи сначала необходимо добавить toohello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="eb3ef-128">Выберите **+ новый шаг** действие hello tooadd хотелось бы tootake при обнаружении нового твит #Seattle</span><span class="sxs-lookup"><span data-stu-id="eb3ef-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="eb3ef-129">![Изображение 1. Действие Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="eb3ef-130">Выберите hello **добавить условие** ссылку.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="eb3ef-131">![Изображение 1. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="eb3ef-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="eb3ef-132">При этом откроется hello **условие** управления, где можно проверять условия, такие как *равен*, *— меньше, чем*, *больше, чем*, *содержит*и т. д.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="eb3ef-133">![Изображение 2. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="eb3ef-134">Выберите hello **выберите значение** элемента управления.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="eb3ef-135">В этом элементе управления можно выбрать одно или несколько свойств hello из предыдущих действиях или триггеров как hello значение, которое будет вычисленное tootrue или false.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="eb3ef-136">![Изображение 3. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="eb3ef-137">Выберите hello **...**  tooexpand hello список свойств, чтобы можно было видеть все доступные свойства hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="eb3ef-138">![Изображение 4. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="eb3ef-139">Выберите hello **число последователи** свойство.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="eb3ef-140">![Изображение 5. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="eb3ef-141">Обратите внимание, свойство count находится в элемент управления значения hello последователи hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Изображение 6: условие Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="eb3ef-143">Выберите **больше, чем** из списка операторов hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="eb3ef-144">![Изображение 7. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="eb3ef-145">Введите 50 как hello операнд для hello *больше, чем* оператор.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="eb3ef-146">Теперь добавляется условие Hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-146">hello condition is now added.</span></span> <span data-ttu-id="eb3ef-147">Сохраните данные с помощью hello **Сохранить** ссылку в меню "hello" выше.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="eb3ef-148">![Изображение 8. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="eb3ef-149">Использование действия Twitter</span><span class="sxs-lookup"><span data-stu-id="eb3ef-149">Use a Twitter action</span></span>
<span data-ttu-id="eb3ef-150">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="eb3ef-151">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="eb3ef-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="eb3ef-152">Теперь, когда вы добавили триггер, выполните эти действия tooadd действия, которая получит новый твит hello содержимое твиты hello найден триггером hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="eb3ef-153">Для целей данного обучения hello будет учитываться только твиты у пользователей с более чем 50 последователи.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="eb3ef-154">В следующем шаге hello вы добавите Twitter действие, которое будет учитывать твит с помощью свойств каждого отправленного пользователем, который имеет более чем 50 последователи твит hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="eb3ef-155">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-155">Select **Add an action**.</span></span> <span data-ttu-id="eb3ef-156">При этом откроется hello управления поиска, где можно найти другие действия и триггеры.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="eb3ef-157">![Изображение 9. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="eb3ef-158">Введите *twitter* в поле поиска hello выберите hello **Twitter - Post твит** действия.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="eb3ef-159">Откроется hello **Post твит** управления можно будет ввести все сведения для учитываемых твит hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="eb3ef-160">![Изображения 1–5. Действие Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="eb3ef-161">Выберите hello **твит текст** элемента управления.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="eb3ef-162">Будут отображены все выходные данные предыдущих действий и триггеров в приложение логику hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="eb3ef-163">Можно выбрать любой из этих и использовать их как часть текст hello твит новый твит hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="eb3ef-164">![Действие Twitter, изображение 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="eb3ef-165">Выберите **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-165">Select **User name**</span></span>   
5. <span data-ttu-id="eb3ef-166">Введите *говорит:* в элементе управления текст твит hello.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="eb3ef-167">Это фразу нужно ввести сразу после имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="eb3ef-168">Выберите *Tweet text* (Текст твита).</span><span class="sxs-lookup"><span data-stu-id="eb3ef-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="eb3ef-169">![Действие Twitter, изображение 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="eb3ef-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="eb3ef-170">Сохраните свою работу и отправки твитов с tooactivate хэштегом hello #Seattle рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="eb3ef-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="eb3ef-171">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="eb3ef-171">Connector-specific details</span></span>

<span data-ttu-id="eb3ef-172">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="eb3ef-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eb3ef-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb3ef-173">Next steps</span></span>
[<span data-ttu-id="eb3ef-174">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="eb3ef-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

