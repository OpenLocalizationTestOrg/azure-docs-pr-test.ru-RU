---
title: "Соединитель базы данных Oracle aaaAdd hello в свои приложения логики Azure | Документы Microsoft"
description: "Использовать соединитель базы данных Oracle hello в приложение логики"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="5768c-103">Начало работы с соединителем hello базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="5768c-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="5768c-104">Используя соединитель hello базы данных Oracle, создать организации рабочие процессы, использующие данные в существующей базе данных.</span><span class="sxs-lookup"><span data-stu-id="5768c-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="5768c-105">Этот соединитель может подключаться tooan установке базы данных Oracle в локальной или виртуальной машине Azure с базой данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="5768c-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="5768c-106">С помощью соединителя вы можете:</span><span class="sxs-lookup"><span data-stu-id="5768c-106">With this connector, you can:</span></span>

* <span data-ttu-id="5768c-107">Сборки рабочего процесса, добавив новую базу данных клиентам tooa клиента или обновления заказа в базе данных заказов.</span><span class="sxs-lookup"><span data-stu-id="5768c-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="5768c-108">Используйте действия tooget строки данных, вставить новую строку и даже удалять.</span><span class="sxs-lookup"><span data-stu-id="5768c-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="5768c-109">Например, создание записи в Dynamics CRM Online (триггер) может приводить к добавлению строки в базу данных Oracle (действие).</span><span class="sxs-lookup"><span data-stu-id="5768c-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="5768c-110">В этом разделе показано, как toouse hello соединителю базы данных Oracle в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5768c-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5768c-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5768c-111">Prerequisites</span></span>

* <span data-ttu-id="5768c-112">Поддерживаемые версии Oracle:</span><span class="sxs-lookup"><span data-stu-id="5768c-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="5768c-113">Oracle 9 и более поздних версий;</span><span class="sxs-lookup"><span data-stu-id="5768c-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="5768c-114">клиентское программное обеспечение Oracle 8.1.7 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="5768c-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="5768c-115">Установите hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="5768c-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="5768c-116">[Подключение tooon локальные данные из приложения логики](../logic-apps/logic-apps-gateway-connection.md) списки hello действия.</span><span class="sxs-lookup"><span data-stu-id="5768c-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="5768c-117">шлюз Hello — tooan tooconnect требуется локальная база данных Oracle или Виртуальной машине Azure с установлена база данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="5768c-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="5768c-118">Hello локального шлюза данных выступает в качестве моста и предоставляет безопасную передачу данных между локальными данными (данные, находится не в облаке hello) и приложениях для логики.</span><span class="sxs-lookup"><span data-stu-id="5768c-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="5768c-119">Здравствуйте, один шлюз может использоваться с несколькими службами и несколько источников данных.</span><span class="sxs-lookup"><span data-stu-id="5768c-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="5768c-120">Таким образом может достаточно шлюза hello tooinstall один раз.</span><span class="sxs-lookup"><span data-stu-id="5768c-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="5768c-121">Установите клиент Oracle hello на машине hello, где установлен на локальный шлюз данных hello.</span><span class="sxs-lookup"><span data-stu-id="5768c-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="5768c-122">Убедитесь, что tooinstall hello 64-разрядный поставщик данных Oracle для .NET из Oracle:</span><span class="sxs-lookup"><span data-stu-id="5768c-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="5768c-123">ODAC 12c, 64-разрядная версия 4 (12.1.0.2.4) для Windows x64</span><span class="sxs-lookup"><span data-stu-id="5768c-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="5768c-124">Если не установлен клиент Oracle hello, произошла ошибка при попытке toocreate или использовать подключение hello.</span><span class="sxs-lookup"><span data-stu-id="5768c-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="5768c-125">В разделе hello типичных ошибок в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5768c-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="5768c-126">Добавление соединителя hello</span><span class="sxs-lookup"><span data-stu-id="5768c-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5768c-127">Этот соединитель не содержит триггеров.</span><span class="sxs-lookup"><span data-stu-id="5768c-127">This connector does not have any triggers.</span></span> <span data-ttu-id="5768c-128">В нем есть только действия.</span><span class="sxs-lookup"><span data-stu-id="5768c-128">It has only actions.</span></span> <span data-ttu-id="5768c-129">Таким образом при создании логики приложения, добавьте другой триггер toostart логику приложения, такие как **расписание - повторения**, или **запрос / ответ - ответ**.</span><span class="sxs-lookup"><span data-stu-id="5768c-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="5768c-130">В hello [портал Azure](https://portal.azure.com), создание пустого логику приложения.</span><span class="sxs-lookup"><span data-stu-id="5768c-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="5768c-131">Во время запуска hello логики приложения, выберите hello **запрос / ответ - запрос** триггер:</span><span class="sxs-lookup"><span data-stu-id="5768c-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="5768c-132">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5768c-132">Select **Save**.</span></span> <span data-ttu-id="5768c-133">При сохранении данных автоматически создается URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="5768c-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="5768c-134">Выберите **Новый шаг**, а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="5768c-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="5768c-135">Введите в `oracle` toosee hello доступных действий:</span><span class="sxs-lookup"><span data-stu-id="5768c-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="5768c-136">Кроме того, это самый быстрый способ toosee hello hello триггеров и действий, доступных для всех соединителей.</span><span class="sxs-lookup"><span data-stu-id="5768c-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="5768c-137">Введите часть имени соединителя hello, такие как `oracle`.</span><span class="sxs-lookup"><span data-stu-id="5768c-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="5768c-138">Конструктор Hello указаны какие-либо триггеры и каких-либо действий.</span><span class="sxs-lookup"><span data-stu-id="5768c-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="5768c-139">Выберите одно из действий hello, таких как **базы данных Oracle - Get строки**.</span><span class="sxs-lookup"><span data-stu-id="5768c-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="5768c-140">Установите флажок **Connect via on-premises data gateway** (Подключение через локальный шлюз данных).</span><span class="sxs-lookup"><span data-stu-id="5768c-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="5768c-141">Введите имя сервера Oracle hello, метод проверки подлинности, имя пользователя, пароль и выберите hello шлюза:</span><span class="sxs-lookup"><span data-stu-id="5768c-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="5768c-142">После подключения выберите таблицу из списка hello и введите идентификатор tooyour hello строки таблицы.</span><span class="sxs-lookup"><span data-stu-id="5768c-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="5768c-143">Требуется идентификатор toohello tooknow hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="5768c-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="5768c-144">Если вы не знаете, обратитесь к администратору базы данных Oracle и получить hello выходные данные `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="5768c-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="5768c-145">Это дает hello сведения, необходимые tooproceed.</span><span class="sxs-lookup"><span data-stu-id="5768c-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="5768c-146">В следующем примере hello задания данных возвращается из базы данных трудовых ресурсов:</span><span class="sxs-lookup"><span data-stu-id="5768c-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="5768c-147">В следующем шаге вы можно использовать любой из hello другие соединители toobuild рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="5768c-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="5768c-148">Если вы tootest получение данных из Oracle, а затем отправить себе электронное сообщение hello Oracle с данными с помощью одного из hello отправьте соединители электронной почты, такие Office 365 или Gmail.</span><span class="sxs-lookup"><span data-stu-id="5768c-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="5768c-149">Используйте маркеры динамических hello из таблицы toobuild hello Oracle hello `Subject` и `Body` вашей электронной почты:</span><span class="sxs-lookup"><span data-stu-id="5768c-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="5768c-150">**Сохраните** приложение логики, а затем выберите **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="5768c-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="5768c-151">Закройте конструктор hello и просмотрите журнал запусков hello статуса hello.</span><span class="sxs-lookup"><span data-stu-id="5768c-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="5768c-152">В случае неудачи, выделите строку неудачное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="5768c-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="5768c-153">Откроется конструктор Hello и показывает, что шаг выполнен и просмотреть hello сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5768c-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="5768c-154">В случае успеха, вы должны получить электронное сообщение hello сведения, которые вы добавили.</span><span class="sxs-lookup"><span data-stu-id="5768c-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="5768c-155">Идеи для рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="5768c-155">Workflow ideas</span></span>

* <span data-ttu-id="5768c-156">Хотите хэштегом hello #oracle toomonitor и поместить твиты hello в базе данных, их можно запросить и использовать в других приложениях.</span><span class="sxs-lookup"><span data-stu-id="5768c-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="5768c-157">В приложении логики, добавить hello `Twitter - When a new tweet is posted` триггер и введите hello **#oracle** хэштегом.</span><span class="sxs-lookup"><span data-stu-id="5768c-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="5768c-158">Затем добавьте hello `Oracle Database - Insert row` действие и выберите таблицу:</span><span class="sxs-lookup"><span data-stu-id="5768c-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="5768c-159">Сообщения отправляются в очередь Service Bus tooa.</span><span class="sxs-lookup"><span data-stu-id="5768c-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="5768c-160">Необходимо tooget эти сообщения и поместить их в базе данных.</span><span class="sxs-lookup"><span data-stu-id="5768c-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="5768c-161">В приложении логики, добавить hello `Service Bus - when a message is received in a queue` триггер и выберите hello очереди.</span><span class="sxs-lookup"><span data-stu-id="5768c-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="5768c-162">Затем добавьте hello `Oracle Database - Insert row` действие и выберите таблицу:</span><span class="sxs-lookup"><span data-stu-id="5768c-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="5768c-163">Распространенные ошибки</span><span class="sxs-lookup"><span data-stu-id="5768c-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="5768c-164">**Ошибка**: не удается связаться с hello шлюза</span><span class="sxs-lookup"><span data-stu-id="5768c-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="5768c-165">**Причина**: hello локальный шлюз данных не может tooconnect toohello облака.</span><span class="sxs-lookup"><span data-stu-id="5768c-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="5768c-166">**Устранение рисков**: Убедитесь, что шлюз находится под управлением hello на локальном компьютере, где он установлен, и что он может подключаться toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="5768c-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="5768c-167">Рекомендуется не устанавливать hello шлюза на компьютере, могут быть отключены или спящего режима.</span><span class="sxs-lookup"><span data-stu-id="5768c-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="5768c-168">Можно также перезапустить службы шлюза данных локальной hello (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="5768c-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="5768c-169">**Ошибка**: используемого поставщика hello устарел: "System.Data.OracleClient требуется клиентское программное обеспечение версии 8.1.7 или более поздней.".</span><span class="sxs-lookup"><span data-stu-id="5768c-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="5768c-170">Перейдите на страницу [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello официальным поставщиком.</span><span class="sxs-lookup"><span data-stu-id="5768c-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="5768c-171">**Причина**: SDK не установлен на компьютере hello там, где hello клиента Oracle hello локальный шлюз данных работает.</span><span class="sxs-lookup"><span data-stu-id="5768c-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="5768c-172">**Разрешение**: Загрузите и установите пакет SDK для клиента Oracle hello на hello компьютере hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="5768c-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="5768c-173">**Ошибка.** В таблице [Имя_таблицы] не определены ключевые столбцы.</span><span class="sxs-lookup"><span data-stu-id="5768c-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="5768c-174">**Причина**: hello таблица имеет первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="5768c-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="5768c-175">**Разрешение**: hello базы данных Oracle соединитель требует использования таблицы со столбцом первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="5768c-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="5768c-176">Сейчас не поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="5768c-176">Currently not supported</span></span>

* <span data-ttu-id="5768c-177">представления и хранимые процедуры;</span><span class="sxs-lookup"><span data-stu-id="5768c-177">Views and stored procedures</span></span> 
* <span data-ttu-id="5768c-178">таблицы с составными ключами;</span><span class="sxs-lookup"><span data-stu-id="5768c-178">Any table with composite keys</span></span>
* <span data-ttu-id="5768c-179">типы вложенных объектов в таблицах.</span><span class="sxs-lookup"><span data-stu-id="5768c-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="5768c-180">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="5768c-180">Connector-specific details</span></span>

<span data-ttu-id="5768c-181">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="5768c-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="5768c-182">Справочные сведения</span><span class="sxs-lookup"><span data-stu-id="5768c-182">Get some help</span></span>

<span data-ttu-id="5768c-183">Hello [приложения логики Azure форум](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) лучшие поместите tooask вопросы, ответить на вопросы и см. другие приложения логики их действия.</span><span class="sxs-lookup"><span data-stu-id="5768c-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="5768c-184">Вы можете улучшить Logic Apps и соединители, внеся свои предложения или проголосовав за уже внесенные на сайте [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="5768c-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5768c-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5768c-185">Next steps</span></span>
<span data-ttu-id="5768c-186">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md)и просмотрите доступные соединители hello в приложениях для логики в наших [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5768c-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
