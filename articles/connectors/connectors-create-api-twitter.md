---
title: "Как использовать соединитель Twitter в приложениях логики | Документация Майкрософт"
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="3c2f9-103">Приступая к работе с соединителем Twitter</span><span class="sxs-lookup"><span data-stu-id="3c2f9-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="3c2f9-104">С помощью соединителя Twitter вы можете:</span><span class="sxs-lookup"><span data-stu-id="3c2f9-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="3c2f9-105">публиковать и получать твиты;</span><span class="sxs-lookup"><span data-stu-id="3c2f9-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="3c2f9-106">получать доступ к временным шкалам, просматривать друзей и подписчиков;</span><span class="sxs-lookup"><span data-stu-id="3c2f9-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="3c2f9-107">выполнять все действия и триггеры, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="3c2f9-108">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="3c2f9-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="3c2f9-110">Подключение к Twitter</span><span class="sxs-lookup"><span data-stu-id="3c2f9-110">Connect to Twitter</span></span>
<span data-ttu-id="3c2f9-111">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="3c2f9-112">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="3c2f9-113">Создание подключения к Twitter</span><span class="sxs-lookup"><span data-stu-id="3c2f9-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="3c2f9-114">Использование триггера Twitter</span><span class="sxs-lookup"><span data-stu-id="3c2f9-114">Use a Twitter trigger</span></span>
<span data-ttu-id="3c2f9-115">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="3c2f9-116">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="3c2f9-117">В этом примере продемонстрировано, как с помощью триггера **When a new tweet is posted** (При публикации нового твита) выполнить поиск по хэш-тегу #Seattle, а затем заменить содержимое файла в Dropbox текстом из твита, отвечающего критериям поиска.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="3c2f9-118">В качестве примера для компаний можно выполнить поиск по имени компании и заменить содержимое базы данных SQL текстом из твита.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="3c2f9-119">В конструкторе приложений логики в поле поиска введите *twitter*, а затем выберите триггер Twitter **When a new tweet is posted** (При публикации нового твита).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="3c2f9-120">![Изображение 1. Триггер Twitter](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="3c2f9-121">В элементе управления **Поиск текста** введите *#Seattle*.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="3c2f9-122">![Изображение 2. Триггер Twitter](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="3c2f9-123">На этом этапе для приложения логики настроен триггер, который будет запускать другие триггеры и действия в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="3c2f9-124">Чтобы приложение логики функционировало, оно должно содержать по крайней мере один триггер и одно действие.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="3c2f9-125">Шаги по добавлению действия описаны в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="3c2f9-126">Добавить условие</span><span class="sxs-lookup"><span data-stu-id="3c2f9-126">Add a condition</span></span>
<span data-ttu-id="3c2f9-127">Так как нас интересуют только твиты от пользователей, у которых более 50 подписчиков, условие, проверяющее число подписчиков, необходимо первым добавить в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="3c2f9-128">Нажмите кнопку **+ Новый шаг**, чтобы добавить действие, которое будет выполняться при обнаружении нового твита с хэш-тегом #Seattle.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="3c2f9-129">![Изображение 1. Действие Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="3c2f9-130">Щелкните ссылку **Добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="3c2f9-131">![Изображение 1. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="3c2f9-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="3c2f9-132">Откроется элемент управления **Условие**, где можно выбрать необходимое условие, например *равно*, *меньше*, *больше*, *содержит* и т. д.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="3c2f9-133">![Изображение 2. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="3c2f9-134">Выберите элемент управления **Выберите значение**.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="3c2f9-135">В этом элементе управления можно выбрать одно или несколько свойств из предыдущих действий или триггеров в качестве значения, которое будет проверяться на соответствие условию (true или false).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="3c2f9-136">![Изображение 3. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="3c2f9-137">Щелкните **…**, чтобы развернуть список всех доступных свойств.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="3c2f9-138">![Изображение 4. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="3c2f9-139">Выберите свойство **Followers count** (Число подписчиков).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="3c2f9-140">![Изображение 5. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="3c2f9-141">Обратите внимание, что теперь свойство "Followers count" (Число подписчиков) отображается в поле выбора значения.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Изображение 6: условие Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="3c2f9-143">Из списка операторов выберите значение **больше**.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="3c2f9-144">![Изображение 7. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="3c2f9-145">Введите 50 в качестве операнда для оператора *больше*.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="3c2f9-146">Условие добавлено.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-146">The condition is now added.</span></span> <span data-ttu-id="3c2f9-147">Чтобы сохранить изменения, щелкните ссылку **Сохранить** в меню вверху.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="3c2f9-148">![Изображение 8. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="3c2f9-149">Использование действия Twitter</span><span class="sxs-lookup"><span data-stu-id="3c2f9-149">Use a Twitter action</span></span>
<span data-ttu-id="3c2f9-150">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="3c2f9-151">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="3c2f9-152">Добавив триггер, выполните следующие шаги, чтобы добавить действие для публикации нового твита с содержимым твитов, найденных с помощью триггера.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="3c2f9-153">Для целей этого пошагового руководства будут публиковаться только твиты пользователей, у которых более 50 подписчиков.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="3c2f9-154">На следующем этапе необходимо добавить действие Twitter для публикации твита с использованием некоторых свойств каждого твита, опубликованного пользователями, у которых более 50 подписчиков.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="3c2f9-155">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-155">Select **Add an action**.</span></span> <span data-ttu-id="3c2f9-156">Откроется элемент управления "Поиск", с помощью которого можно найти другие действия и триггеры.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="3c2f9-157">![Изображение 9. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="3c2f9-158">В поле поиска введите *twitter*, а затем выберите действие Twitter **Post a tweet** (Публикация твита).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="3c2f9-159">Откроется элемент управления **Post a tweet** (Публикация твита), где необходимо добавить все сведения о твите, который публикуется.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="3c2f9-160">![Изображения 1–5. Действие Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="3c2f9-161">Выберите элемент управления **Tweet text** (Текст твита).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="3c2f9-162">Отобразятся все выходные данные из предыдущих действий и триггеров в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="3c2f9-163">Эти данные можно использовать в качестве текста нового твита.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="3c2f9-164">![Действие Twitter, изображение 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="3c2f9-165">Выберите **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-165">Select **User name**</span></span>   
5. <span data-ttu-id="3c2f9-166">В текстовом поле элемента управления "Tweet text" (Текст твита) введите *says:*.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="3c2f9-167">Это фразу нужно ввести сразу после имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="3c2f9-168">Выберите *Tweet text* (Текст твита).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="3c2f9-169">![Действие Twitter, изображение 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="3c2f9-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="3c2f9-170">Сохраните изменения и активируйте рабочий процесс путем отправки твита с хэш-тегом #Seattle.</span><span class="sxs-lookup"><span data-stu-id="3c2f9-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="3c2f9-171">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="3c2f9-171">Connector-specific details</span></span>

<span data-ttu-id="3c2f9-172">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="3c2f9-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3c2f9-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c2f9-173">Next steps</span></span>
[<span data-ttu-id="3c2f9-174">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="3c2f9-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

