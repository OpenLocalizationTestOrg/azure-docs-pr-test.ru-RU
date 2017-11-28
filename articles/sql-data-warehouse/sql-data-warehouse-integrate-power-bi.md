---
title: "Использование Power BI с хранилищем данных SQL | Документация Майкрософт"
description: "Советы по использованию Power BI с хранилищем данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="86b80-103">Использование Power BI с хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="86b80-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="86b80-104">Так же как при работе с базой данных SQL Azure, функция прямого соединения хранилища данных SQL позволяет использовать аналитические возможности Power BI.</span><span class="sxs-lookup"><span data-stu-id="86b80-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="86b80-105">Прямое соединение позволяет отправлять запросы в хранилище данных SQL Azure в режиме реального времени по мере исследования данных.</span><span class="sxs-lookup"><span data-stu-id="86b80-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="86b80-106">Благодаря этому в сочетании с масштабом хранилища данных SQL пользователи могут за считаные минуты создавать динамические отчеты на основе терабайтов данных.</span><span class="sxs-lookup"><span data-stu-id="86b80-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="86b80-107">Кроме того, появление кнопки "Открыть в Power BI" дает возможность пользователям подключить Power BI напрямую к хранилищу данных SQL, не собирая сведений из других частей Azure.</span><span class="sxs-lookup"><span data-stu-id="86b80-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="86b80-108">При использовании прямого соединения следует обратить внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="86b80-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="86b80-109">Указывайте полное имя сервера при подключении (дополнительные сведения см. ниже).</span><span class="sxs-lookup"><span data-stu-id="86b80-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="86b80-110">Убедитесь, что правила брандмауэра для базы данных имеют настройку "Разрешить доступ к службам Azure".</span><span class="sxs-lookup"><span data-stu-id="86b80-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="86b80-111">Каждое действие, например выбор столбца или добавление фильтра, отправляет запрос напрямую в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="86b80-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="86b80-112">Плитки обновляются примерно каждые 15 минут (обновление не нужно планировать).</span><span class="sxs-lookup"><span data-stu-id="86b80-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="86b80-113">Раздел вопросов и ответов недоступен для наборов данных прямого соединения.</span><span class="sxs-lookup"><span data-stu-id="86b80-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="86b80-114">Изменения схемы не выбираются автоматически.</span><span class="sxs-lookup"><span data-stu-id="86b80-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="86b80-115">Время ожидания любых запросов на прямое соединение истекает через две минуты.</span><span class="sxs-lookup"><span data-stu-id="86b80-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="86b80-116">Эти ограничения и примечания могут быть изменены по мере улучшения работы продуктов.</span><span class="sxs-lookup"><span data-stu-id="86b80-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="86b80-117">Ниже описаны действия по подключению.</span><span class="sxs-lookup"><span data-stu-id="86b80-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="86b80-118">Подключение с помощью кнопки "Открыть в Power BI"</span><span class="sxs-lookup"><span data-stu-id="86b80-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="86b80-119">Самый простой способ перемещаться между хранилищем данных SQL и Power BI — использовать кнопку "Открыть в Power BI".</span><span class="sxs-lookup"><span data-stu-id="86b80-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="86b80-120">Эта кнопка позволяет легко создавать новые панели мониторинга в Power BI.</span><span class="sxs-lookup"><span data-stu-id="86b80-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="86b80-121">Чтобы начать работу, перейдите в экземпляр хранилища данных SQL на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="86b80-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="86b80-122">Нажмите кнопку «Открыть в Power BI».</span><span class="sxs-lookup"><span data-stu-id="86b80-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="86b80-123">Если войти напрямую не получается или у вас нет учетной записи Power BI, необходимо выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="86b80-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="86b80-124">Вы будете перенаправлены на страницу подключения хранилища данных SQL, при этом некоторые сведения из хранилища данных SQL будут уже указаны.</span><span class="sxs-lookup"><span data-stu-id="86b80-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="86b80-125">После ввода учетных данных выполняется полное подключение к хранилищу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="86b80-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="86b80-126">Подключение через портал Power BI</span><span class="sxs-lookup"><span data-stu-id="86b80-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="86b80-127">Помимо подключения с помощью кнопки "Открыть в Power BI", пользователи могут подключаться к хранилищу данных SQL через портал Power BI.</span><span class="sxs-lookup"><span data-stu-id="86b80-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="86b80-128">Щелкните «Получить данные» в нижней части области навигации.</span><span class="sxs-lookup"><span data-stu-id="86b80-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="86b80-129">Выберите «Базы данных».</span><span class="sxs-lookup"><span data-stu-id="86b80-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="86b80-130">На странице «Базы данных» выберите «Хранилище данных SQL Azure» и нажмите кнопку «Подключиться».</span><span class="sxs-lookup"><span data-stu-id="86b80-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="86b80-131">Введите данные, необходимые для подключения.</span><span class="sxs-lookup"><span data-stu-id="86b80-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="86b80-132">Имя сервера и имя базы данных можно посмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="86b80-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="86b80-133">Вы вернетесь на главную страницу Power BI, и после установления подключения в списке «Наборы данных» появится новая запись с именем вашего экземпляра.</span><span class="sxs-lookup"><span data-stu-id="86b80-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="86b80-134">Вы можете щелкнуть новый набор данных, чтобы изучить все таблицы и представления в базе данных.</span><span class="sxs-lookup"><span data-stu-id="86b80-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="86b80-135">При выборе столбца отправляется запрос обратно источнику и динамически создается визуальный элемент.</span><span class="sxs-lookup"><span data-stu-id="86b80-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="86b80-136">Визуальные элементы можно сохранить в новом отчете и прикрепить к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="86b80-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
