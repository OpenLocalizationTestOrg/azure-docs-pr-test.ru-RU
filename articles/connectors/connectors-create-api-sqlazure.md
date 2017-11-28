---
title: "Соединитель базы данных SQL Azure aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Обзор соединителя базы данных SQL Azure с параметрами интерфейса REST API"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="0a77b-103">Начало работы с соединителем hello базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0a77b-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="0a77b-104">С помощью соединителя hello базы данных SQL Azure, создайте рабочие процессы для вашей организации, работающие с данными в таблицах.</span><span class="sxs-lookup"><span data-stu-id="0a77b-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="0a77b-105">С помощью базы данных SQL вы можете:</span><span class="sxs-lookup"><span data-stu-id="0a77b-105">With SQL Database, you:</span></span>

* <span data-ttu-id="0a77b-106">Сборки рабочего процесса, добавив новую базу данных клиентам tooa клиента или обновления заказа в базе данных заказов.</span><span class="sxs-lookup"><span data-stu-id="0a77b-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="0a77b-107">Используйте действия tooget строки данных, вставить новую строку и даже удалять.</span><span class="sxs-lookup"><span data-stu-id="0a77b-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="0a77b-108">Например, при создании записи в Dynamics CRM Online (триггер) может вставляться строка в базу данных SQL Azure (действие).</span><span class="sxs-lookup"><span data-stu-id="0a77b-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="0a77b-109">В этом разделе показано, как toouse hello соединителю базы данных SQL в приложении логику, а также списки hello действия.</span><span class="sxs-lookup"><span data-stu-id="0a77b-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="0a77b-110">toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0a77b-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="0a77b-111">Подключение tooAzure базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="0a77b-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="0a77b-112">Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="0a77b-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="0a77b-113">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="0a77b-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="0a77b-114">Например, tooSQL tooconnect базы данных, создания базы данных SQL *соединения*.</span><span class="sxs-lookup"><span data-stu-id="0a77b-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="0a77b-115">toocreate подключения введите hello учетные данные, обычно используемые tooaccess hello службы, которому вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="0a77b-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="0a77b-116">Таким образом в базе данных SQL, введите подключение hello toocreate учетные данные базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="0a77b-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="0a77b-117">Создайте соединение hello</span><span class="sxs-lookup"><span data-stu-id="0a77b-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="0a77b-118">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="0a77b-118">Use a trigger</span></span>
<span data-ttu-id="0a77b-119">Этот соединитель не содержит триггеров.</span><span class="sxs-lookup"><span data-stu-id="0a77b-119">This connector does not have any triggers.</span></span> <span data-ttu-id="0a77b-120">Использование других триггеров toostart hello логики приложения, например повторения триггера, триггер HTTP веб-перехватчика, триггеры, доступных с другими соединители и многое другое.</span><span class="sxs-lookup"><span data-stu-id="0a77b-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="0a77b-121">Пример см. в статье о [создании приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0a77b-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="0a77b-122">Использование действий</span><span class="sxs-lookup"><span data-stu-id="0a77b-122">Use an action</span></span>
<span data-ttu-id="0a77b-123">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="0a77b-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="0a77b-124">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0a77b-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="0a77b-125">Выберите hello "плюс".</span><span class="sxs-lookup"><span data-stu-id="0a77b-125">Select hello plus sign.</span></span> <span data-ttu-id="0a77b-126">Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.</span><span class="sxs-lookup"><span data-stu-id="0a77b-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="0a77b-127">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="0a77b-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="0a77b-128">В текстовом поле hello введите «sql» tooget список всех доступных действий hello.</span><span class="sxs-lookup"><span data-stu-id="0a77b-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="0a77b-129">В нашем примере мы выберем действие для SQL Server **Get row** (Получение строки).</span><span class="sxs-lookup"><span data-stu-id="0a77b-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="0a77b-130">Если подключение уже существует, то выберите hello **имя таблицы** hello раскрывающемся списке, а затем введите hello **идентификатор строки** требуется tooreturn.</span><span class="sxs-lookup"><span data-stu-id="0a77b-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="0a77b-131">При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения.</span><span class="sxs-lookup"><span data-stu-id="0a77b-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="0a77b-132">[Создайте соединение hello](connectors-create-api-sqlazure.md#create-the-connection) в этом разделе описываются эти свойства.</span><span class="sxs-lookup"><span data-stu-id="0a77b-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0a77b-133">В этом примере строка возвращается из таблицы.</span><span class="sxs-lookup"><span data-stu-id="0a77b-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="0a77b-134">toosee hello данных в этой строке, добавьте другое действие, которое создает файл с помощью hello поля из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="0a77b-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="0a77b-135">Например добавьте OneDrive действие, которое использует hello FirstName и LastName поля toocreate в новом файле в hello учетная запись облачного хранилища.</span><span class="sxs-lookup"><span data-stu-id="0a77b-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="0a77b-136">**Сохранить** изменения (левом верхнем углу панели инструментов hello).</span><span class="sxs-lookup"><span data-stu-id="0a77b-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="0a77b-137">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="0a77b-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="0a77b-138">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="0a77b-138">Connector-specific details</span></span>

<span data-ttu-id="0a77b-139">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="0a77b-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0a77b-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a77b-140">Next steps</span></span>
<span data-ttu-id="0a77b-141">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0a77b-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="0a77b-142">Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0a77b-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

