---
title: "Как использовать соединитель MQ в Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как подключиться к локальному серверу или серверу Azure MQ из рабочего процесса приложения логики для просмотра, получения и отправки сообщений в WebSphere MQ."
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
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="80336-103">Подключение к серверу IBM MQ из приложения логики с помощью соединителя MQ</span><span class="sxs-lookup"><span data-stu-id="80336-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="80336-104">Соединитель с MQ (Microsoft) отправляет и получает сообщения, хранящиеся локально на сервере MQ или в Azure.</span><span class="sxs-lookup"><span data-stu-id="80336-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="80336-105">Этот соединитель включает в себя клиент Microsoft MQ для взаимодействия с удаленным сервером IBM MQ по сети TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="80336-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="80336-106">Этот документ является базовым руководством для использования соединителя MQ.</span><span class="sxs-lookup"><span data-stu-id="80336-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="80336-107">Мы рекомендуем начать с просмотра одного сообщения в очереди, и затем попробовать другие действия.</span><span class="sxs-lookup"><span data-stu-id="80336-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="80336-108">Соединитель MQ позволяет выполнять перечисленные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="80336-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="80336-109">Триггеры отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="80336-109">There are no triggers.</span></span>

-   <span data-ttu-id="80336-110">Просматривать отдельные сообщения, не удаляя их с сервера IBM MQ.</span><span class="sxs-lookup"><span data-stu-id="80336-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="80336-111">Просматривать пакет сообщений, не удаляя сообщения с сервера IBM MQ.</span><span class="sxs-lookup"><span data-stu-id="80336-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="80336-112">Получать отдельные сообщения с сервера IBM MQ и удалять их с сервера.</span><span class="sxs-lookup"><span data-stu-id="80336-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="80336-113">Получать пакет сообщений с сервера IBM MQ и удалять сообщения с сервера.</span><span class="sxs-lookup"><span data-stu-id="80336-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="80336-114">Отправлять отдельные сообщения на сервер IBM MQ.</span><span class="sxs-lookup"><span data-stu-id="80336-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="80336-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="80336-115">Prerequisites</span></span>

* <span data-ttu-id="80336-116">Если используется локальный сервер MQ, то [установите локальный шлюз данных](../logic-apps/logic-apps-gateway-install.md) на сервере в пределах сети.</span><span class="sxs-lookup"><span data-stu-id="80336-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="80336-117">Если сервер MQ является общедоступным или доступным в пределах Azure, то установка шлюза данных не требуется, так как он не используется.</span><span class="sxs-lookup"><span data-stu-id="80336-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="80336-118">Чтобы функционировал соединитель MQ, на сервере, где установлен локальный шлюз данных, также должна быть установлена платформа .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="80336-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="80336-119">Создайте ресурс Azure для локального шлюза данных (см. статью [Доступ к локальным источникам данных из приложений логики с помощью локального шлюза данных](../logic-apps/logic-apps-gateway-connection.md)).</span><span class="sxs-lookup"><span data-stu-id="80336-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="80336-120">Официально поддерживаемые версии IBM WebSphere MQ:</span><span class="sxs-lookup"><span data-stu-id="80336-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="80336-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="80336-121">MQ 7.5</span></span>
   * <span data-ttu-id="80336-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="80336-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="80336-123">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="80336-123">Create a logic app</span></span>

1. <span data-ttu-id="80336-124">На **начальной доске Azure** выберите **+** (знак плюс), **Интернет+мобильные устройства**, а затем — **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="80336-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="80336-125">Укажите **имя**, например MQTestApp, **подписку**, **группу ресурсов**, и **расположение** (используйте расположение, в котором настроено подключение к локальному шлюзу данных).</span><span class="sxs-lookup"><span data-stu-id="80336-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="80336-126">Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="80336-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="80336-127">![Создание приложения логики](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="80336-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="80336-128">Добавление триггера</span><span class="sxs-lookup"><span data-stu-id="80336-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="80336-129">Соединитель MQ не содержит триггеров.</span><span class="sxs-lookup"><span data-stu-id="80336-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="80336-130">Поэтому для запуска приложения логики используйте другой триггер, например **Повторение**.</span><span class="sxs-lookup"><span data-stu-id="80336-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="80336-131">Откройте **конструктор Logic Apps** и в списке часто используемых триггеров выберите **Повторение**.</span><span class="sxs-lookup"><span data-stu-id="80336-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="80336-132">В триггере "Повторение" нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="80336-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="80336-133">В поле **Частота** выберите **День**, а в поле **Интервал** введите **7**.</span><span class="sxs-lookup"><span data-stu-id="80336-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="80336-134">Просмотр одного сообщения</span><span class="sxs-lookup"><span data-stu-id="80336-134">Browse a single message</span></span>
1. <span data-ttu-id="80336-135">Выберите **+ Новый шаг**, а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="80336-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="80336-136">В поле поиска введите `mq`, а затем выберите **MQ - Browse message** (MQ — просмотр сообщения).</span><span class="sxs-lookup"><span data-stu-id="80336-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="80336-137">![Просмотр сообщения](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="80336-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="80336-138">Если отсутствует подключение к MQ, то создайте его:</span><span class="sxs-lookup"><span data-stu-id="80336-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="80336-139">Выберите **Connect via on-premises data gateway** (Подключение через локальный шлюз данных) и введите свойства сервера MQ.</span><span class="sxs-lookup"><span data-stu-id="80336-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="80336-140">В поле **Сервер** укажите имя сервера MQ или введите IP-адрес, после него поставьте двоеточие, а затем укажите номер порта.</span><span class="sxs-lookup"><span data-stu-id="80336-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="80336-141">В раскрывающемся списке **Шлюз** перечислены все существующие подключения шлюза, которые были настроены.</span><span class="sxs-lookup"><span data-stu-id="80336-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="80336-142">Выберите шлюз.</span><span class="sxs-lookup"><span data-stu-id="80336-142">Select your gateway.</span></span>
    3. <span data-ttu-id="80336-143">По завершении нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="80336-143">Select **Create** when finished.</span></span> <span data-ttu-id="80336-144">Подключение выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="80336-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="80336-145">![Свойства подключения](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="80336-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="80336-146">В свойствах действия предоставляются следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="80336-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="80336-147">Используйте свойство **Очередь**, чтобы выбрать имя очереди, отличное от того, которое определено в подключении.</span><span class="sxs-lookup"><span data-stu-id="80336-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="80336-148">Используйте свойства **MessageId**, **CorrelationId**, **GroupId** и другие, чтобы найти сообщение на основе различных свойств сообщений MQ.</span><span class="sxs-lookup"><span data-stu-id="80336-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="80336-149">Задайте для свойства **IncludeInfo** значение **True**, чтобы включить в выходные данные дополнительные сведения о сообщении.</span><span class="sxs-lookup"><span data-stu-id="80336-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="80336-150">Либо задайте значение **False**, чтобы не включать в выходные данные эти сведения.</span><span class="sxs-lookup"><span data-stu-id="80336-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="80336-151">Введите значение **времени ожидания**, чтобы определить, как долго ожидать получения сообщения в пустой очереди.</span><span class="sxs-lookup"><span data-stu-id="80336-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="80336-152">Если это значение не задано, то извлекается первое сообщение в очереди, и, следовательно, время на ожидание сообщения не тратится.</span><span class="sxs-lookup"><span data-stu-id="80336-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="80336-153">![Просмотр сообщения: свойства](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="80336-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="80336-154">**Сохраните** изменения, а затем щелкните **Выполнить**, чтобы запустить приложение логики:</span><span class="sxs-lookup"><span data-stu-id="80336-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="80336-155">![Сохранение и запуск](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="80336-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="80336-156">Через несколько секунд отображаются шаги выполнения, и можно посмотреть выходные данные.</span><span class="sxs-lookup"><span data-stu-id="80336-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="80336-157">Щелкните зеленый флажок, чтобы просмотреть подобные сведения о каждом шаге.</span><span class="sxs-lookup"><span data-stu-id="80336-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="80336-158">Выберите **Посмотреть необработанные выходные данные**, чтобы просмотреть дополнительные сведения о выходных данных.</span><span class="sxs-lookup"><span data-stu-id="80336-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="80336-159">![Просмотр сообщения: выходные данные](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="80336-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="80336-160">Необработанные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="80336-160">Raw output:</span></span>  
    ![Просмотр сообщения: необработанные выходные данные](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="80336-162">Если для свойства **IncludeInfo** задано значение true, то отобразятся следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="80336-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="80336-163">![Просмотр сообщения: IncludeInfo](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="80336-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="80336-164">Просмотр нескольких сообщений</span><span class="sxs-lookup"><span data-stu-id="80336-164">Browse multiple messages</span></span>
<span data-ttu-id="80336-165">Действие **Browse messages** (Просмотреть сообщения) имеет свойство **BatchSize** (Размер пакета). Оно указывает, сколько сообщений должно быть возвращено из очереди.</span><span class="sxs-lookup"><span data-stu-id="80336-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="80336-166">Если для свойства **BatchSize** значение не задано, то возвращаются все сообщения.</span><span class="sxs-lookup"><span data-stu-id="80336-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="80336-167">Возвращаемые выходные данные представляют собой массив сообщений.</span><span class="sxs-lookup"><span data-stu-id="80336-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="80336-168">При добавлении действия **Browse messages** (Просмотреть сообщения) по умолчанию выбирается подключение, которое было настроено первым.</span><span class="sxs-lookup"><span data-stu-id="80336-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="80336-169">Щелкните **Изменить подключение**, чтобы создать подключение или выбрать другое существующее подключение.</span><span class="sxs-lookup"><span data-stu-id="80336-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="80336-170">Выходные данные действия "Browse messages" (Просмотреть сообщения) имеют такой вид:</span><span class="sxs-lookup"><span data-stu-id="80336-170">The output of Browse messages shows:</span></span>  
![Просмотр сообщений: выходные данные](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="80336-172">Получение одного сообщения</span><span class="sxs-lookup"><span data-stu-id="80336-172">Receive a single message</span></span>
<span data-ttu-id="80336-173">Действие **Получить сообщение** имеет такие входные и выходные данные, что и действие **Browse message** (Просмотреть сообщение).</span><span class="sxs-lookup"><span data-stu-id="80336-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="80336-174">При использовании действия **Получить сообщение** это сообщение удаляется из очереди.</span><span class="sxs-lookup"><span data-stu-id="80336-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="80336-175">Получение нескольких сообщений</span><span class="sxs-lookup"><span data-stu-id="80336-175">Receive multiple messages</span></span>
<span data-ttu-id="80336-176">Действие **Получить сообщения** имеет такие входные и выходные данные, что и действие **Browse messages** (Просмотреть сообщения).</span><span class="sxs-lookup"><span data-stu-id="80336-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="80336-177">При использовании действия **Получить сообщения** эти сообщения удаляются из очереди.</span><span class="sxs-lookup"><span data-stu-id="80336-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="80336-178">Если при выполнении действия просмотра или получения в очереди не будет сообщений, то действие завершится сбоем и отобразятся следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="80336-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![Ошибка MQ при отсутствии сообщений](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="80336-180">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="80336-180">Send a message</span></span>
1. <span data-ttu-id="80336-181">При добавлении действия **Отправить сообщение** по умолчанию выбирается подключение, которое было настроено первым.</span><span class="sxs-lookup"><span data-stu-id="80336-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="80336-182">Щелкните **Изменить подключение**, чтобы создать подключение или выбрать другое существующее подключение.</span><span class="sxs-lookup"><span data-stu-id="80336-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="80336-183">Допустимые **типы сообщений**: **датаграмма**, **ответ** и **запрос**.</span><span class="sxs-lookup"><span data-stu-id="80336-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="80336-184">![Свойства отправки сообщения](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="80336-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="80336-185">Выходные данные действия "Отправить сообщение" выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="80336-185">The output of Send message looks like the following:</span></span>  
![Отправить сообщение: выходные данные](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="80336-187">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="80336-187">Connector-specific details</span></span>

<span data-ttu-id="80336-188">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="80336-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80336-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80336-189">Next steps</span></span>
<span data-ttu-id="80336-190">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="80336-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="80336-191">Чтобы узнать, какие еще соединители доступны в Logic Apps, просмотрите [список интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="80336-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
