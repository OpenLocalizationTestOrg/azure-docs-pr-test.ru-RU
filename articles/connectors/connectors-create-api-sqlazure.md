---
title: "Добавление соединителя базы данных SQL Azure в приложения логики | Документация Майкрософт"
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="39ae2-103">Начало работы с соединителем базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="39ae2-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="39ae2-104">С помощью соединителя базы данных SQL Azure можно создавать рабочие процессы для управления данными в таблицах в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="39ae2-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="39ae2-105">С помощью базы данных SQL вы можете:</span><span class="sxs-lookup"><span data-stu-id="39ae2-105">With SQL Database, you:</span></span>

* <span data-ttu-id="39ae2-106">создавать рабочие процессы путем добавления нового клиента в базу данных клиентов или обновления заказа в базе данных заказов;</span><span class="sxs-lookup"><span data-stu-id="39ae2-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="39ae2-107">использовать действия для получения строки данных, вставки новой строки и даже ее удаления.</span><span class="sxs-lookup"><span data-stu-id="39ae2-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="39ae2-108">Например, при создании записи в Dynamics CRM Online (триггер) может вставляться строка в базу данных SQL Azure (действие).</span><span class="sxs-lookup"><span data-stu-id="39ae2-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="39ae2-109">В этой статье содержатся сведения об использовании соединителя базы данных SQL в приложении логики, а также перечислены предоставляемые им действия.</span><span class="sxs-lookup"><span data-stu-id="39ae2-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="39ae2-110">Дополнительные сведения о приложениях логики см. в статье, посвященной [приложениям логики](../logic-apps/logic-apps-what-are-logic-apps.md), и [руководстве по созданию приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="39ae2-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="39ae2-111">Подключение к базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="39ae2-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="39ae2-112">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="39ae2-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="39ae2-113">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="39ae2-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="39ae2-114">Например, чтобы подключиться к базе данных SQL, сначала необходимо создать соответствующее *подключение*.</span><span class="sxs-lookup"><span data-stu-id="39ae2-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="39ae2-115">Чтобы создать подключение, нужно ввести учетные данные, которые используются для доступа к определенной службе.</span><span class="sxs-lookup"><span data-stu-id="39ae2-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="39ae2-116">Таким образом, чтобы создать подключение к базе данных SQL, введите учетные данные базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="39ae2-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="39ae2-117">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="39ae2-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="39ae2-118">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="39ae2-118">Use a trigger</span></span>
<span data-ttu-id="39ae2-119">Этот соединитель не содержит триггеров.</span><span class="sxs-lookup"><span data-stu-id="39ae2-119">This connector does not have any triggers.</span></span> <span data-ttu-id="39ae2-120">Чтобы запустить приложение логики, используйте другие триггеры, например триггер повторения, триггер веб-перехватчика HTTP, триггеры, доступные для других соединителей, и другие.</span><span class="sxs-lookup"><span data-stu-id="39ae2-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="39ae2-121">Пример см. в статье о [создании приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="39ae2-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="39ae2-122">Использование действий</span><span class="sxs-lookup"><span data-stu-id="39ae2-122">Use an action</span></span>
<span data-ttu-id="39ae2-123">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="39ae2-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="39ae2-124">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="39ae2-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="39ae2-125">Щелкните знак "плюс".</span><span class="sxs-lookup"><span data-stu-id="39ae2-125">Select the plus sign.</span></span> <span data-ttu-id="39ae2-126">Отобразятся следующие команды: **Добавить действие**, **Добавить условие** или **Еще**.</span><span class="sxs-lookup"><span data-stu-id="39ae2-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="39ae2-127">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="39ae2-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="39ae2-128">Чтобы открыть список всех доступных действий, в текстовом поле введите sql.</span><span class="sxs-lookup"><span data-stu-id="39ae2-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="39ae2-129">В нашем примере мы выберем действие для SQL Server **Get row** (Получение строки).</span><span class="sxs-lookup"><span data-stu-id="39ae2-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="39ae2-130">Если подключение уже существует, выберите **имя таблицы** в раскрывающемся списке и введите **идентификатор строки**, который необходимо вернуть.</span><span class="sxs-lookup"><span data-stu-id="39ae2-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="39ae2-131">Если появится запрос на предоставление сведений о подключении, введите их, чтобы создать подключение.</span><span class="sxs-lookup"><span data-stu-id="39ae2-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="39ae2-132">Эти свойства описаны в разделе о [создании подключения](connectors-create-api-sqlazure.md#create-the-connection) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="39ae2-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="39ae2-133">В этом примере строка возвращается из таблицы.</span><span class="sxs-lookup"><span data-stu-id="39ae2-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="39ae2-134">Чтобы просмотреть данные в этой строке, добавьте другое действие, которое создает файл с помощью полей из таблицы.</span><span class="sxs-lookup"><span data-stu-id="39ae2-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="39ae2-135">Например, можно добавить действие OneDrive, использующее поля FirstName и LastName, чтобы создать файл в учетной записи облачного хранилища.</span><span class="sxs-lookup"><span data-stu-id="39ae2-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="39ae2-136">**Сохраните** изменения, нажав соответствующую кнопку в левом верхнем углу панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="39ae2-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="39ae2-137">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="39ae2-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="39ae2-138">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="39ae2-138">Connector-specific details</span></span>

<span data-ttu-id="39ae2-139">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="39ae2-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="39ae2-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39ae2-140">Next steps</span></span>
<span data-ttu-id="39ae2-141">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="39ae2-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="39ae2-142">Чтобы узнать, какие еще соединители доступны в Logic Apps, просмотрите [список интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="39ae2-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

