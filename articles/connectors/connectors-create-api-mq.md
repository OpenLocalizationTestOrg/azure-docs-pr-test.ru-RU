---
title: "aaaLearn как toouse hello MQ соединителя в приложения логики Azure | Документы Microsoft"
description: "Подключение tooan в локальной среде или Azure MQ сервер из вашего toobrowse логику приложения рабочего процесса, получения и отправки сообщений tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="227ef-103">Подключение tooan IBM MQ сервера из логики приложения с помощью соединителя MQ hello</span><span class="sxs-lookup"><span data-stu-id="227ef-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="227ef-104">Соединитель с MQ (Microsoft) отправляет и получает сообщения, хранящиеся локально на сервере MQ или в Azure.</span><span class="sxs-lookup"><span data-stu-id="227ef-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="227ef-105">Этот соединитель включает в себя клиент Microsoft MQ для взаимодействия с удаленным сервером IBM MQ по сети TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="227ef-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="227ef-106">В этом документе — это соединитель MQ руководство toouse начальный hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="227ef-107">Рекомендуется начать с просмотра одно сообщение в очередь и повторить hello других действий.</span><span class="sxs-lookup"><span data-stu-id="227ef-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="227ef-108">Соединитель MQ Hello включает hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="227ef-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="227ef-109">Триггеры отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="227ef-109">There are no triggers.</span></span>

-   <span data-ttu-id="227ef-110">Обзор одного сообщения без удаления приветственное сообщение от сервера IBM MQ hello</span><span class="sxs-lookup"><span data-stu-id="227ef-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="227ef-111">Обзор пакета сообщений без удаления сообщений hello из hello IBM MQ сервера</span><span class="sxs-lookup"><span data-stu-id="227ef-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="227ef-112">Получение одного сообщения и удаление приветственное сообщение из hello IBM MQ сервера</span><span class="sxs-lookup"><span data-stu-id="227ef-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="227ef-113">Получать пакет сообщений и удаление сообщений hello из hello IBM MQ сервера</span><span class="sxs-lookup"><span data-stu-id="227ef-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="227ef-114">Отправка одного сообщения toohello IBM MQ сервера</span><span class="sxs-lookup"><span data-stu-id="227ef-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="227ef-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="227ef-115">Prerequisites</span></span>

* <span data-ttu-id="227ef-116">При использовании локального сервера MQ [установить шлюз данных в локальной среде hello](../logic-apps/logic-apps-gateway-install.md) на сервере в сети.</span><span class="sxs-lookup"><span data-stu-id="227ef-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="227ef-117">Если hello MQ Server публично доступные или доступна в Azure, затем шлюз данных hello не используемые и не требуется.</span><span class="sxs-lookup"><span data-stu-id="227ef-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="227ef-118">Hello сервера, где hello устанавливается на локальный шлюз данных также должен иметь .net Framework 4.6 для соединителя MQ toofunction hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="227ef-119">Создать hello ресурсов Azure для hello локальный шлюз данных — [Настройка подключения шлюза данных hello](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="227ef-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="227ef-120">Официально поддерживаемые версии IBM WebSphere MQ:</span><span class="sxs-lookup"><span data-stu-id="227ef-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="227ef-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="227ef-121">MQ 7.5</span></span>
   * <span data-ttu-id="227ef-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="227ef-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="227ef-123">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="227ef-123">Create a logic app</span></span>

1. <span data-ttu-id="227ef-124">В hello **Azure запустить плата**выберите  **+**  (плюс), **Интернет + мобильные устройства**, а затем **приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="227ef-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="227ef-125">Введите hello **имя**, такие как MQTestApp, **подписки**, **группы ресурсов**, и **расположение** (используйте hello расположение, где hello локальный шлюз данных подключение было настроено).</span><span class="sxs-lookup"><span data-stu-id="227ef-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="227ef-126">Выберите **toodashboard ПИН-код**и выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="227ef-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="227ef-127">![Создание приложения логики](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="227ef-128">Добавление триггера</span><span class="sxs-lookup"><span data-stu-id="227ef-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="227ef-129">Hello MQ Connector не поддерживает какие-либо триггеры.</span><span class="sxs-lookup"><span data-stu-id="227ef-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="227ef-130">Таким образом, используйте другой триггер toostart логику приложения, такие как hello **повторения** триггера.</span><span class="sxs-lookup"><span data-stu-id="227ef-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="227ef-131">Hello **логику приложения конструктор** откроется, выберите **повторения** в список общих триггеров hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="227ef-132">Выберите **изменить** внутри hello повторения триггера.</span><span class="sxs-lookup"><span data-stu-id="227ef-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="227ef-133">Набор hello **частоты** слишком**день**и набор hello **интервал** слишком**7**.</span><span class="sxs-lookup"><span data-stu-id="227ef-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="227ef-134">Просмотр одного сообщения</span><span class="sxs-lookup"><span data-stu-id="227ef-134">Browse a single message</span></span>
1. <span data-ttu-id="227ef-135">Выберите **+ Новый шаг**, а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="227ef-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="227ef-136">Введите в поле поиска hello `mq`и выберите **MQ - обзора сообщение**.</span><span class="sxs-lookup"><span data-stu-id="227ef-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="227ef-137">![Просмотр сообщения](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="227ef-138">Если нет существующего подключения MQ, затем создайте hello подключение:</span><span class="sxs-lookup"><span data-stu-id="227ef-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="227ef-139">Выберите **подключиться через локальный шлюз данных**и введите свойства hello MQ сервера.</span><span class="sxs-lookup"><span data-stu-id="227ef-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="227ef-140">Для **сервера**, введите имя сервера MQ hello или ввести hello IP-адрес с номером порта, двоеточие и hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="227ef-141">Hello **шлюза** раскрывающемся списке перечислены все текущие подключения шлюза, которые были настроены.</span><span class="sxs-lookup"><span data-stu-id="227ef-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="227ef-142">Выберите шлюз.</span><span class="sxs-lookup"><span data-stu-id="227ef-142">Select your gateway.</span></span>
    3. <span data-ttu-id="227ef-143">По завершении нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="227ef-143">Select **Create** when finished.</span></span> <span data-ttu-id="227ef-144">Подключение к выглядит примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="227ef-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="227ef-145">![Свойства подключения](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="227ef-146">Свойства действия hello вы можете:</span><span class="sxs-lookup"><span data-stu-id="227ef-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="227ef-147">Используйте hello **очереди** tooaccess свойство имени разные очереди, чем сеть, определенная в соединении hello</span><span class="sxs-lookup"><span data-stu-id="227ef-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="227ef-148">Используйте hello **MessageId**, **CorrelationId**, **GroupId**и другие свойства toobrowse для сообщения на основании свойства сообщения другой MQ hello</span><span class="sxs-lookup"><span data-stu-id="227ef-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="227ef-149">Задать **IncludeInfo** слишком**True** tooinclude дополнительное сообщение сведения в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="227ef-150">Или задайте для него слишком**False** toonot включить дополнительные сообщения в выходные данные hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="227ef-151">Введите **время ожидания** toodetermine значение как долго toowait для tooarrive сообщения в пустом списке ожидания.</span><span class="sxs-lookup"><span data-stu-id="227ef-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="227ef-152">Если ничего не указано, получить hello первого сообщения в очереди hello и есть нет время ожидания tooappear сообщения.</span><span class="sxs-lookup"><span data-stu-id="227ef-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="227ef-153">![Просмотр сообщения: свойства](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="227ef-154">**Сохраните** изменения, а затем щелкните **Выполнить**, чтобы запустить приложение логики:</span><span class="sxs-lookup"><span data-stu-id="227ef-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="227ef-155">![Сохранение и запуск](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="227ef-156">Через несколько секунд hello объекта hello выполнения шагов, и можно посмотреть на вывод hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="227ef-157">Выберите hello зеленой галочкой toosee подробные сведения каждого этапа.</span><span class="sxs-lookup"><span data-stu-id="227ef-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="227ef-158">Выберите **необработанные выходные данные в разделе** toosee Дополнительные сведения о hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="227ef-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="227ef-159">![Просмотр сообщения: выходные данные](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="227ef-160">Необработанные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="227ef-160">Raw output:</span></span>  
    ![Просмотр сообщения: необработанные выходные данные](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="227ef-162">Здравствуйте, когда **IncludeInfo** tootrue был установлен, отображается hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="227ef-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="227ef-163">![Просмотр сообщения: IncludeInfo](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="227ef-164">Просмотр нескольких сообщений</span><span class="sxs-lookup"><span data-stu-id="227ef-164">Browse multiple messages</span></span>
<span data-ttu-id="227ef-165">Hello **просмотра сообщений о** действие включает **BatchSize** tooindicate параметр должен возвращаться количество сообщений из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="227ef-166">Если для свойства **BatchSize** значение не задано, то возвращаются все сообщения.</span><span class="sxs-lookup"><span data-stu-id="227ef-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="227ef-167">Hello вернул выходных данных представляет собой массив сообщений.</span><span class="sxs-lookup"><span data-stu-id="227ef-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="227ef-168">При добавлении hello **просмотра сообщений о** действие hello первого подключения, настроенного по умолчанию установлен.</span><span class="sxs-lookup"><span data-stu-id="227ef-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="227ef-169">Выберите **изменить подключение** toocreate новое соединение, или выберите другое подключение.</span><span class="sxs-lookup"><span data-stu-id="227ef-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="227ef-170">выходные данные Hello обзора сообщений показано:</span><span class="sxs-lookup"><span data-stu-id="227ef-170">hello output of Browse messages shows:</span></span>  
![Просмотр сообщений: выходные данные](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="227ef-172">Получение одного сообщения</span><span class="sxs-lookup"><span data-stu-id="227ef-172">Receive a single message</span></span>
<span data-ttu-id="227ef-173">Hello **получить сообщение** действие имеет hello же входные и выходные данные как hello **сообщение обзора** действие.</span><span class="sxs-lookup"><span data-stu-id="227ef-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="227ef-174">При использовании **получить сообщение**, приветственное сообщение удаляется из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="227ef-175">Получение нескольких сообщений</span><span class="sxs-lookup"><span data-stu-id="227ef-175">Receive multiple messages</span></span>
<span data-ttu-id="227ef-176">Hello **получать сообщения** действие имеет hello же входные и выходные данные как hello **просмотра сообщений о** действие.</span><span class="sxs-lookup"><span data-stu-id="227ef-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="227ef-177">При использовании **получать сообщения**, hello сообщения удаляются из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="227ef-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="227ef-178">Если нет сообщений в очереди hello при выполнении browse или инструкция receive, hello шаг завершается ошибкой с hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="227ef-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![Ошибка MQ при отсутствии сообщений](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="227ef-180">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="227ef-180">Send a message</span></span>
1. <span data-ttu-id="227ef-181">При добавлении hello **отправляемого сообщения** действие hello первого подключения, настроенного по умолчанию установлен.</span><span class="sxs-lookup"><span data-stu-id="227ef-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="227ef-182">Выберите **изменить подключение** toocreate новое соединение, или выберите другое подключение.</span><span class="sxs-lookup"><span data-stu-id="227ef-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="227ef-183">Допустимые Hello **типы сообщений** , **датаграмм**, **ответ**, или **запроса**.</span><span class="sxs-lookup"><span data-stu-id="227ef-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="227ef-184">![Свойства отправки сообщения](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="227ef-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="227ef-185">Hello выходные данные отправляемого сообщения выглядят hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="227ef-185">hello output of Send message looks like hello following:</span></span>  
![Отправить сообщение: выходные данные](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="227ef-187">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="227ef-187">Connector-specific details</span></span>

<span data-ttu-id="227ef-188">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="227ef-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="227ef-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="227ef-189">Next steps</span></span>
<span data-ttu-id="227ef-190">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="227ef-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="227ef-191">Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="227ef-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
