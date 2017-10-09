---
title: "aaaConnect tooAzure хранилище данных SQL - SSMS | Документы Microsoft"
description: "Используйте SQL Server Management Studio (SSMS) tooconnect tooand запрос хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="76a9f-103">Подключение tooSQL хранилища данных с SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="76a9f-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76a9f-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="76a9f-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="76a9f-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="76a9f-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="76a9f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="76a9f-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="76a9f-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="76a9f-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="76a9f-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="76a9f-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="76a9f-109">Используйте SQL Server Management Studio (SSMS) tooconnect tooand запрос хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="76a9f-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76a9f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="76a9f-110">Prerequisites</span></span>
<span data-ttu-id="76a9f-111">toouse этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="76a9f-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="76a9f-112">Существующее хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="76a9f-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="76a9f-113">разделе toocreate, [создать хранилище данных SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="76a9f-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="76a9f-114">Установленный SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="76a9f-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="76a9f-115">[Установите SSMS][Install SSMS] бесплатно, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="76a9f-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="76a9f-116">Hello полное доменное имя сервера SQL server.</span><span class="sxs-lookup"><span data-stu-id="76a9f-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="76a9f-117">toofind это, см. в разделе [подключения хранилища данных tooSQL][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="76a9f-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="76a9f-118">1. Подключение tooyour хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="76a9f-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="76a9f-119">Откройте среду SSMS.</span><span class="sxs-lookup"><span data-stu-id="76a9f-119">Open SSMS.</span></span>
2. <span data-ttu-id="76a9f-120">Откройте обозреватель объектов.</span><span class="sxs-lookup"><span data-stu-id="76a9f-120">Open Object Explorer.</span></span> <span data-ttu-id="76a9f-121">toodo это, выберите **файл** > **подключить к обозревателю объектов**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Обозреватель объектов SQL Server][1]
3. <span data-ttu-id="76a9f-123">Заполните поля hello в окне tooServer Connect hello.</span><span class="sxs-lookup"><span data-stu-id="76a9f-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Подключение tooServer][2]
   
   * <span data-ttu-id="76a9f-125">**Имя сервера**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-125">**Server name**.</span></span> <span data-ttu-id="76a9f-126">Введите hello **имя сервера** ранее определенных.</span><span class="sxs-lookup"><span data-stu-id="76a9f-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="76a9f-127">**Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-127">**Authentication**.</span></span> <span data-ttu-id="76a9f-128">Выберите **Проверка подлинности SQL Server** или **Встроенная проверка подлинности Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="76a9f-129">**Имя пользователя** и **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-129">**User Name** and **Password**.</span></span> <span data-ttu-id="76a9f-130">Если вы выбрали проверку подлинности SQL Server, введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="76a9f-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="76a9f-131">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-131">Click **Connect**.</span></span>
4. <span data-ttu-id="76a9f-132">tooexplore, разверните сервер Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="76a9f-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="76a9f-133">Вы можете просмотреть hello баз данных, связанных с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="76a9f-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="76a9f-134">Разверните AdventureWorksDW toosee hello таблицам образца базы данных.</span><span class="sxs-lookup"><span data-stu-id="76a9f-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Обзор AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="76a9f-136">2) Запуск пробного запроса</span><span class="sxs-lookup"><span data-stu-id="76a9f-136">2. Run a sample query</span></span>
<span data-ttu-id="76a9f-137">Теперь, когда соединение было tooyour установленной базы данных, давайте написать запрос.</span><span class="sxs-lookup"><span data-stu-id="76a9f-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="76a9f-138">Щелкните правой кнопкой мыши базу данных в обозревателе объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="76a9f-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="76a9f-139">Выберите пункт **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="76a9f-139">Select **New Query**.</span></span> <span data-ttu-id="76a9f-140">Откроется окно нового запроса.</span><span class="sxs-lookup"><span data-stu-id="76a9f-140">A new query window opens.</span></span>
   
    ![Создать запрос][4]
3. <span data-ttu-id="76a9f-142">Скопируйте этот запрос TSQL в окно запроса hello:</span><span class="sxs-lookup"><span data-stu-id="76a9f-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="76a9f-143">Выполните запрос hello.</span><span class="sxs-lookup"><span data-stu-id="76a9f-143">Run hello query.</span></span> <span data-ttu-id="76a9f-144">toodo, нажмите кнопку `Execute` или hello используйте следующий ярлык: `F5`.</span><span class="sxs-lookup"><span data-stu-id="76a9f-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Выполнение запроса][5]
5. <span data-ttu-id="76a9f-146">Взгляните на результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="76a9f-146">Look at hello query results.</span></span> <span data-ttu-id="76a9f-147">В этом примере таблицы FactInternetSales hello содержит 60398 строк.</span><span class="sxs-lookup"><span data-stu-id="76a9f-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Результаты запроса][6]

## <a name="next-steps"></a><span data-ttu-id="76a9f-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76a9f-149">Next steps</span></span>
<span data-ttu-id="76a9f-150">Теперь, когда вы сможете подключиться и запросов, попробуйте [визуализация данных hello с PowerBI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="76a9f-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="76a9f-151">tooconfigure среды для проверки подлинности Azure Active Directory, в разделе [tooSQL хранилища данных проверки подлинности][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="76a9f-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
