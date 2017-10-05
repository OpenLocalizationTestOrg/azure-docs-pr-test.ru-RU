---
title: "Подключение к хранилищу данных SQL Azure — VSTS | Документация Майкрософт"
description: "Отправка запросов к хранилищу данных SQL с помощью Visual Studio."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="7781c-103">Подключение к хранилищу данных SQL с помощью Visual Studio и SSDT</span><span class="sxs-lookup"><span data-stu-id="7781c-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7781c-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="7781c-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="7781c-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="7781c-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="7781c-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7781c-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="7781c-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="7781c-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="7781c-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="7781c-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="7781c-109">В Visual Studio можно отправлять запросы к хранилищу данных SQL Azure за считанные минуты.</span><span class="sxs-lookup"><span data-stu-id="7781c-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="7781c-110">В этом методе используется расширение SQL Server Data Tools (SSDT) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7781c-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7781c-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7781c-111">Prerequisites</span></span>
<span data-ttu-id="7781c-112">Для работы с этим руководством необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="7781c-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="7781c-113">Существующее хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7781c-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="7781c-114">Сведения о его создании см. в статье [Создание хранилища данных SQL Azure][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="7781c-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="7781c-115">Расширение SSDT для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7781c-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="7781c-116">Скорее всего, оно уже есть, если на вашем компьютере установлено приложение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7781c-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="7781c-117">Инструкции по установке и доступные варианты установки см. в статье [Установка Visual Studio 2015 и SSDT для хранилища данных SQL][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="7781c-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="7781c-118">Полное имя сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7781c-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="7781c-119">Эти сведения можно узнать в статье [Подключение к хранилищу данных SQL Azure][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="7781c-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="7781c-120">1. Подключение к хранилищу данных SQL</span><span class="sxs-lookup"><span data-stu-id="7781c-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="7781c-121">Откройте Visual Studio 2013 или 2015.</span><span class="sxs-lookup"><span data-stu-id="7781c-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="7781c-122">Откройте обозреватель объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7781c-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="7781c-123">Чтобы сделать это, выберите **Представление** > **Обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7781c-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Обозреватель объектов SQL Server][1]
3. <span data-ttu-id="7781c-125">Щелкните значок **Добавить SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="7781c-125">Click the **Add SQL Server** icon.</span></span>
   
    ![Добавить SQL Server][2]
4. <span data-ttu-id="7781c-127">Заполните поля в окне «Подключение к серверу».</span><span class="sxs-lookup"><span data-stu-id="7781c-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Подключение к серверу][3]
   
   * <span data-ttu-id="7781c-129">**Имя сервера**.</span><span class="sxs-lookup"><span data-stu-id="7781c-129">**Server name**.</span></span> <span data-ttu-id="7781c-130">Введите найденное **имя сервера** .</span><span class="sxs-lookup"><span data-stu-id="7781c-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="7781c-131">**Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="7781c-131">**Authentication**.</span></span> <span data-ttu-id="7781c-132">Выберите **Проверка подлинности SQL Server** или **Встроенная проверка подлинности Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7781c-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="7781c-133">**Имя пользователя** и **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7781c-133">**User Name** and **Password**.</span></span> <span data-ttu-id="7781c-134">Если вы выбрали проверку подлинности SQL Server, введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7781c-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="7781c-135">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="7781c-135">Click **Connect**.</span></span>
5. <span data-ttu-id="7781c-136">Чтобы исследовать данные, разверните сервер Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7781c-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="7781c-137">Вы можете просмотреть базы данных, связанные с сервером.</span><span class="sxs-lookup"><span data-stu-id="7781c-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="7781c-138">Разверните AdventureWorksDW, чтобы просмотреть таблицы в образце базы данных.</span><span class="sxs-lookup"><span data-stu-id="7781c-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Обзор AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="7781c-140">2) Запуск пробного запроса</span><span class="sxs-lookup"><span data-stu-id="7781c-140">2. Run a sample query</span></span>
<span data-ttu-id="7781c-141">Теперь, когда мы подключились к базе данных, давайте напишем запрос.</span><span class="sxs-lookup"><span data-stu-id="7781c-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="7781c-142">Щелкните правой кнопкой мыши базу данных в обозревателе объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7781c-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="7781c-143">Выберите пункт **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="7781c-143">Select **New Query**.</span></span> <span data-ttu-id="7781c-144">Откроется окно нового запроса.</span><span class="sxs-lookup"><span data-stu-id="7781c-144">A new query window opens.</span></span>
   
    ![Создать запрос][5]
3. <span data-ttu-id="7781c-146">Скопируйте следующий запрос TSQL в окно запроса.</span><span class="sxs-lookup"><span data-stu-id="7781c-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="7781c-147">Выполните запрос.</span><span class="sxs-lookup"><span data-stu-id="7781c-147">Run the query.</span></span> <span data-ttu-id="7781c-148">Для этого щелкните зеленую стрелку или воспользуйтесь сочетанием клавиш `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="7781c-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Выполнение запроса][6]
5. <span data-ttu-id="7781c-150">Просмотрите результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="7781c-150">Look at the query results.</span></span> <span data-ttu-id="7781c-151">В этом примере таблица FactInternetSales содержит 60 398 строк.</span><span class="sxs-lookup"><span data-stu-id="7781c-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Результаты запроса][7]

## <a name="next-steps"></a><span data-ttu-id="7781c-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7781c-153">Next steps</span></span>
<span data-ttu-id="7781c-154">Теперь, когда вы можете подключаться к базе данных и отправлять запросы, попробуйте [визуализировать данные с помощью PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="7781c-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="7781c-155">Сведения о том, как настроить проверку подлинности Azure Active Directory в своей среде, см. в статье [Проверка подлинности в хранилище данных SQL Azure][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="7781c-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
