---
title: "Настройка мониторинга событий с помощью концентраторов событий Azure для Azure Logic Apps | Документация Майкрософт"
description: "Мониторинг потоков данных, передающих события между Azure Logic Apps и концентраторами событий Azure"
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
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="1c252-104">Мониторинг, получение и отправка событий с помощью соединителя концентратора событий</span><span class="sxs-lookup"><span data-stu-id="1c252-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="1c252-105">Чтобы настроить мониторинг событий, предоставляя приложениям логики возможность обнаруживать, получать и отправлять события, подключитесь из приложения логики к [концентратору событий Azure](https://azure.microsoft.com/services/event-hubs).</span><span class="sxs-lookup"><span data-stu-id="1c252-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="1c252-106">Ознакомьтесь с дополнительными сведениями о [концентраторах событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="1c252-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="1c252-107">Требования</span><span class="sxs-lookup"><span data-stu-id="1c252-107">Requirements</span></span>

* <span data-ttu-id="1c252-108">Вам потребуется [пространство имен концентраторов событий и концентратор событий](../event-hubs/event-hubs-create.md) в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c252-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="1c252-109">Узнайте, как [создать пространство имен концентраторов событий и концентратор событий](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1c252-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="1c252-110">Прежде чем добавлять в приложение логики [соединители](https://docs.microsoft.com/azure/connectors/apis-list), нужно сначала создать само приложение логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="1c252-111">Узнайте, как [создать приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1c252-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="1c252-112">Проверка разрешений для пространства имен концентраторов событий и определение строки подключения</span><span class="sxs-lookup"><span data-stu-id="1c252-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="1c252-113">Чтобы приложение логики получило доступ к любой службе, следует создать [*подключение*](./connectors-overview.md) между приложением логики и этой службой (если вы еще не сделали это).</span><span class="sxs-lookup"><span data-stu-id="1c252-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="1c252-114">Такое подключение предоставит приложению логики права на доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="1c252-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="1c252-115">Чтобы приложение логики могло использовать концентратор событий, у вас должны быть права на **управление** и строка подключения для доступа к пространству имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1c252-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="1c252-116">Чтобы проверить наличие разрешений и получить строку подключения, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1c252-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="1c252-117">Войдите на [портал Azure](https://portal.azure.com "Портал Azure").</span><span class="sxs-lookup"><span data-stu-id="1c252-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="1c252-118">Перейдите к *пространству имен* концентраторов событий (но не к конкретному концентратору событий).</span><span class="sxs-lookup"><span data-stu-id="1c252-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="1c252-119">В колонке пространства имен в разделе **Параметры** выберите **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="1c252-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="1c252-120">В разделе **Утверждения** убедитесь, что у вас есть разрешения на **управление** для этого пространства имен.</span><span class="sxs-lookup"><span data-stu-id="1c252-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Управление разрешениями для пространства имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="1c252-122">Чтобы скопировать строку подключения к пространству имен концентраторов событий, выберите **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="1c252-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="1c252-123">Теперь нажмите кнопку копирования рядом со строкой подключения первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="1c252-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Скопируйте строку подключения к пространству имен концентраторов событий](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="1c252-125">Чтобы проверить, относится ли строка подключения к пространству имен концентраторов событий или к определенному концентратору событий, попробуйте найти в ней параметр `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="1c252-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="1c252-126">Если в строке подключения есть такой параметр, значит она относится к определенной сущности концентратора событий, и ее нельзя использовать в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="1c252-127">Когда вам будет предложено ввести учетные после добавления триггеров или действий концентраторов событий в приложение логики, вы сможете подключиться к пространству имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1c252-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="1c252-128">Присвойте имя созданному подключению, введите скопированную ранее строку подключения и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c252-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Ввод строки подключения к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="1c252-130">Когда вы завершите создание подключения, его имя появится в соответствующем триггере или действии концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1c252-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="1c252-131">Теперь можно переходить к другим действиям в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-131">You can then continue with the other steps in your logic app.</span></span>

    ![Созданное подключение к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="1c252-133">Запуск рабочего процесса при получении новых событий от концентратора событий</span><span class="sxs-lookup"><span data-stu-id="1c252-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="1c252-134">[*Триггер*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) — это событие, которое запускает рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="1c252-135">Чтобы рабочий процесс запускался при отправке нового события в концентратор событий, добавьте триггер для обнаружения событий, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="1c252-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="1c252-136">На [портале Azure](https://portal.azure.com "портал Azure ") перейдите к существующему приложению логики или создайте пустое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="1c252-137">В конструкторе Logic Apps введите в поле поиска текст фильтра `event hubs`.</span><span class="sxs-lookup"><span data-stu-id="1c252-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="1c252-138">Выберите триггер с именем **При наличии событий в концентраторе событий**.</span><span class="sxs-lookup"><span data-stu-id="1c252-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Выбор триггера, срабатывающего при получении концентратором событий новых событий](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="1c252-140">Если у вас еще нет подключения к пространству имен концентраторов событий, вам будет предложено создать такое подключение.</span><span class="sxs-lookup"><span data-stu-id="1c252-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="1c252-141">Присвойте имя этому подключению и введите строку подключения к пространству имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1c252-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="1c252-142">Если вы не знаете, как найти строку подключения, см. [инструкции в этом разделе](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="1c252-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Ввод строки подключения к пространству имен концентраторов событий](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="1c252-144">После создания подключения вы увидите параметры для настройки триггера **При наличии событий в концентраторе событий**.</span><span class="sxs-lookup"><span data-stu-id="1c252-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Настройки триггера, срабатывающего при получении концентратором событий новых событий](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="1c252-146">Укажите имя концентратора событий, который требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="1c252-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="1c252-147">Укажите частоту и продолжительность проверки этого концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="1c252-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="1c252-148">Если вы хотите выбрать группу потребителей для чтения событий, нажмите действие **Показать дополнительные параметры** (необязательно).</span><span class="sxs-lookup"><span data-stu-id="1c252-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Выбор концентратора событий или группы потребителей](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="1c252-150">Теперь у вас есть настроенный триггер для запуска рабочего процесса приложения логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="1c252-151">Приложение логики проверяет указанный концентратор событий, используя созданное вами расписание.</span><span class="sxs-lookup"><span data-stu-id="1c252-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="1c252-152">Если приложение обнаруживает новые события в концентраторе событий, этот триггер запускает другие действия или триггеры в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="1c252-153">Отправка событий в концентратор событий из приложения логики</span><span class="sxs-lookup"><span data-stu-id="1c252-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="1c252-154">[*Действие*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) — это задание, выполняемое рабочим процессом приложения логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="1c252-155">После добавления триггера в приложение логики вы можете добавить действие, выполняющее операции с данными, созданными этим триггером.</span><span class="sxs-lookup"><span data-stu-id="1c252-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="1c252-156">Чтобы отправлять события в концентратор событий из приложения логики, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1c252-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="1c252-157">В конструкторе Logic App выберите для созданного триггера приложения логики пункты **Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="1c252-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Выбор действий "Новый шаг" и "Добавить действие"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="1c252-159">Теперь найдите и выберите нужное действие.</span><span class="sxs-lookup"><span data-stu-id="1c252-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="1c252-160">Здесь вы можете выбрать любое доступное действие, но для нашего примера мы выберем действие отправки событий в концентраторы событий.</span><span class="sxs-lookup"><span data-stu-id="1c252-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="1c252-161">В поле поиска введите текст `event hubs` для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="1c252-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="1c252-162">Выберите действие **Отправка события**.</span><span class="sxs-lookup"><span data-stu-id="1c252-162">Select this action: **Send event**</span></span>

    ![Выбор действия "Концентраторы событий — отправка события"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="1c252-164">Введите обязательные сведения для этого события, например имя концентратора событий, в который вы будете отправлять событие.</span><span class="sxs-lookup"><span data-stu-id="1c252-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="1c252-165">Введите любые необязательные сведения о событии, например описание.</span><span class="sxs-lookup"><span data-stu-id="1c252-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="1c252-166">Если вы хотите указать раздел концентратора событий, в который следует отправлять событие, выберите **Показать дополнительные параметры** (необязательно).</span><span class="sxs-lookup"><span data-stu-id="1c252-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Ввод имени концентратора событий и необязательных сведений о событии](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="1c252-168">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="1c252-168">Save your changes.</span></span>

    ![Сохранение приложения логики](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="1c252-170">Теперь у вас есть настроенное действие для отправки событий из приложения логики.</span><span class="sxs-lookup"><span data-stu-id="1c252-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="1c252-171">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="1c252-171">Connector-specific details</span></span>

<span data-ttu-id="1c252-172">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="1c252-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="1c252-173">Получение справки</span><span class="sxs-lookup"><span data-stu-id="1c252-173">Get help</span></span>

<span data-ttu-id="1c252-174">Чтобы задать вопросы, помочь другим пользователям и узнать, что делают другие пользователи, посетите [форум по Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1c252-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1c252-175">Чтобы улучшить Logic Apps и соединители, голосуйте за идеи или предлагайте собственные на [сайте обратной связи Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1c252-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c252-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c252-176">Next steps</span></span>

*  <span data-ttu-id="1c252-177">Изучите [список соединителей](./apis-list.md) для приложений логики в Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="1c252-177">[Find other connectors for Azure Logic apps](./apis-list.md)</span></span>