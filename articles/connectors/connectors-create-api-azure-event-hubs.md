---
title: "aaaSet монитор событий концентраторов событий Azure для приложения логики Azure с | Документы Microsoft"
description: "Наблюдения за событиями tooreceive потоки данных и отправки событий для приложения логики Azure с помощью концентраторов событий Azure"
services: logic-apps
keywords: "поток данных, монитор событий, концентраторы событий"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="2bfdc-104">Отслеживание, получать и отправлять события с соединителем hello концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2bfdc-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="2bfdc-105">tooset монитор событий, что логика приложения можно обнаруживать события, получать события и отправлять события, подключения tooan [концентратор событий Azure](https://azure.microsoft.com/services/event-hubs) из логики приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="2bfdc-106">Ознакомьтесь с дополнительными сведениями о [концентраторах событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="2bfdc-107">Требования</span><span class="sxs-lookup"><span data-stu-id="2bfdc-107">Requirements</span></span>

* <span data-ttu-id="2bfdc-108">У вас есть toohave [пространство имен концентраторов событий и концентратора событий](../event-hubs/event-hubs-create.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="2bfdc-109">Дополнительные сведения [как toocreate пространство имен концентраторов событий и концентратора событий](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="2bfdc-110">toouse [всех соединителей](https://docs.microsoft.com/azure/connectors/apis-list) в приложении логику имеется toocreate логику приложение сначала.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="2bfdc-111">Дополнительные сведения [как toocreate приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="2bfdc-112">Проверьте разрешения имен концентраторов событий и найдите строку подключения hello</span><span class="sxs-lookup"><span data-stu-id="2bfdc-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="2bfdc-113">Для вашего tooaccess логику приложения любой службы, имеют toocreate [ *подключения* ](./connectors-overview.md) между логику hello и приложения службы, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="2bfdc-114">Это подключение авторизует данные tooaccess логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="2bfdc-115">Для вашего tooaccess логику приложения концентратора событий, у вас есть toohave **управление** разрешения и hello строку подключения для пространства имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="2bfdc-116">toocheck разрешения и строки подключения hello get, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="2bfdc-117">Войдите в toohello [портал Azure](https://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="2bfdc-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="2bfdc-118">Go концентраторов событий tooyour *имен*, не hello конкретный концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="2bfdc-119">В колонке hello пространства имен в разделе **параметры**, выберите **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="2bfdc-120">В разделе **Утверждения** убедитесь, что у вас есть разрешения на **управление** для этого пространства имен.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Управление разрешениями для пространства имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="2bfdc-122">Выберите строку подключения hello toocopy для пространства имен hello концентраторов событий, **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="2bfdc-123">Далее tooyour первичного ключа строки подключения, выберите "Копировать" hello ".</span><span class="sxs-lookup"><span data-stu-id="2bfdc-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Скопируйте строку подключения к пространству имен концентраторов событий](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="2bfdc-125">tooconfirm ли указана строка соединения, связанного с пространством имен концентраторов событий или с конкретный концентратор событий, проверять hello строку подключения для hello `EntityPath` параметра.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="2bfdc-126">Если этот параметр, hello строка подключения для конкретного концентратора событий «entity» и не toouse правильными hello с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="2bfdc-127">Теперь когда появится запрос учетных данных после добавления концентраторов событий триггера или действие tooyour логику приложения, можно подключиться пространство имен tooyour концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="2bfdc-128">Присвойте имя подключения, введите строку подключения hello, которые скопированы и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Ввод строки подключения к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="2bfdc-130">После создания подключения, имя подключения hello появится в триггер hello концентраторов событий или действия.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="2bfdc-131">После этого можно продолжить с hello других шагов в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Созданное подключение к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="2bfdc-133">Запуск рабочего процесса при получении новых событий от концентратора событий</span><span class="sxs-lookup"><span data-stu-id="2bfdc-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="2bfdc-134">[*Триггер*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) — это событие, которое запускает рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="2bfdc-135">Чтобы запустить рабочий процесс, когда новые события отправляются tooyour концентратора событий, выполните следующие действия для добавления hello триггер, который обнаруживает это событие.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="2bfdc-136">В hello [портал Azure](https://portal.azure.com "портал Azure"), go tooyour существующего логику приложения или создания пустой логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="2bfdc-137">Введите в поле поиска hello для hello конструктор логики приложения, `event hubs` для фильтра.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="2bfdc-138">Выберите триггер с именем **При наличии событий в концентраторе событий**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Выбор триггера, срабатывающего при получении концентратором событий новых событий](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="2bfdc-140">Если у вас еще нет концентраторов событий tooyour пространство имен подключения, вам предложат toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="2bfdc-141">Присвойте имя подключения и введите строку подключения hello концентраторов событий пространства имен.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="2bfdc-142">При необходимости сведения [как toofind строки подключения](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Ввод строки подключения к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="2bfdc-144">После создания соединения hello hello параметры для hello **при возникновении события в концентратор событий** отображаются триггера.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Настройки триггера, срабатывающего при получении концентратором событий новых событий](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="2bfdc-146">Введите или выберите имя hello hello концентратора событий, которые должны toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="2bfdc-147">Выберите частоту hello и интервала для частоту hello toocheck концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="2bfdc-148">toooptionally выберите группу потребителей для чтения событий, выберите **Показывать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Выбор концентратора событий или группы потребителей](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="2bfdc-150">Теперь настройки toostart триггера рабочего процесса для логики приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="2bfdc-151">Логика приложения проверяет hello указан на основе расписания hello, устанавливаемое концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="2bfdc-152">Если приложение находит новые события в концентратор событий hello, другие действия или триггеры выполняется триггер hello в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="2bfdc-153">Отправка событий tooyour концентратор событий из логики приложения</span><span class="sxs-lookup"><span data-stu-id="2bfdc-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="2bfdc-154">[*Действие*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) — это задание, выполняемое рабочим процессом приложения логики.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="2bfdc-155">После добавления в приложение логику tooyour триггера, можно добавить действие tooperform операций с данными, созданный с помощью этого триггера.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="2bfdc-156">toosend tooyour события концентратора событий, от логики приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="2bfdc-157">В конструкторе Logic App выберите для созданного триггера приложения логики пункты **Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Выбор действий "Новый шаг" и "Добавить действие"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="2bfdc-159">Теперь можно найти и выбрать tooperform действие.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="2bfdc-160">Хотя можно выбрать любое действие, например, мы хотим действие toosend hello событий концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="2bfdc-161">Введите в поле поиска hello, `event hubs` для фильтра.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="2bfdc-162">Выберите действие **Отправка события**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-162">Select this action: **Send event**</span></span>

    ![Выбор действия "Концентраторы событий — отправка события"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="2bfdc-164">Введите hello необходимые сведения для события hello, например имя hello hello место toosend hello события концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="2bfdc-165">Введите любые другие дополнительные сведения о событии hello, например содержимого для этого события.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="2bfdc-166">toooptionally указать раздел hello концентратора событий, где toosend hello событий, выберите **Показывать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Ввод имени концентратора событий и необязательных сведений о событии](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="2bfdc-168">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-168">Save your changes.</span></span>

    ![Сохранение приложения логики](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="2bfdc-170">Теперь настройки событий toosend действие с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="2bfdc-171">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="2bfdc-171">Connector-specific details</span></span>

<span data-ttu-id="2bfdc-172">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="2bfdc-173">Получение справки</span><span class="sxs-lookup"><span data-stu-id="2bfdc-173">Get help</span></span>

<span data-ttu-id="2bfdc-174">tooask вопросы, ответы на вопросы и см. какие другие пользователи приложения логики Azure делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="2bfdc-175">toohelp улучшить логику приложений и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2bfdc-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bfdc-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2bfdc-176">Next steps</span></span>

*  <span data-ttu-id="2bfdc-177">Изучите [список соединителей](./apis-list.md) для приложений логики в Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="2bfdc-177">[Find other connectors for Azure Logic apps](./apis-list.md)</span></span>