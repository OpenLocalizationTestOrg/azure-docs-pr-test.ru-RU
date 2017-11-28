---
title: "aaaConnect tooAzure хранилище данных SQL - VSTS | Документы Microsoft"
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="79760-103">Подключиться с помощью Visual Studio и SSDT tooSQL хранилища данных</span><span class="sxs-lookup"><span data-stu-id="79760-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79760-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="79760-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="79760-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="79760-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="79760-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79760-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="79760-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="79760-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="79760-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="79760-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="79760-109">Используйте Visual Studio tooquery хранилище данных SQL Azure через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="79760-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="79760-110">Этот метод использует расширение hello SQL Server Data Tools (SSDT) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79760-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="79760-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79760-111">Prerequisites</span></span>
<span data-ttu-id="79760-112">toouse этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="79760-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="79760-113">Существующее хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="79760-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="79760-114">разделе toocreate, [создать хранилище данных SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="79760-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="79760-115">Расширение SSDT для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79760-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="79760-116">Скорее всего, оно уже есть, если на вашем компьютере установлено приложение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79760-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="79760-117">Инструкции по установке и доступные варианты установки см. в статье [Установка Visual Studio 2015 и SSDT для хранилища данных SQL][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="79760-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="79760-118">Hello полное доменное имя сервера SQL server.</span><span class="sxs-lookup"><span data-stu-id="79760-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="79760-119">toofind это, см. в разделе [подключения хранилища данных tooSQL][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="79760-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="79760-120">1. Подключение tooyour хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="79760-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="79760-121">Откройте Visual Studio 2013 или 2015.</span><span class="sxs-lookup"><span data-stu-id="79760-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="79760-122">Откройте обозреватель объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="79760-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="79760-123">toodo это, выберите **представление** > **обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="79760-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Обозреватель объектов SQL Server][1]
3. <span data-ttu-id="79760-125">Нажмите кнопку hello **добавить SQL Server** значок.</span><span class="sxs-lookup"><span data-stu-id="79760-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Добавить SQL Server][2]
4. <span data-ttu-id="79760-127">Заполните поля hello в окне tooServer Connect hello.</span><span class="sxs-lookup"><span data-stu-id="79760-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Подключение tooServer][3]
   
   * <span data-ttu-id="79760-129">**Имя сервера**.</span><span class="sxs-lookup"><span data-stu-id="79760-129">**Server name**.</span></span> <span data-ttu-id="79760-130">Введите hello **имя сервера** ранее определенных.</span><span class="sxs-lookup"><span data-stu-id="79760-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="79760-131">**Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="79760-131">**Authentication**.</span></span> <span data-ttu-id="79760-132">Выберите **Проверка подлинности SQL Server** или **Встроенная проверка подлинности Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79760-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="79760-133">**Имя пользователя** и **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="79760-133">**User Name** and **Password**.</span></span> <span data-ttu-id="79760-134">Если вы выбрали проверку подлинности SQL Server, введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="79760-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="79760-135">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="79760-135">Click **Connect**.</span></span>
5. <span data-ttu-id="79760-136">tooexplore, разверните сервер Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="79760-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="79760-137">Вы можете просмотреть hello баз данных, связанных с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="79760-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="79760-138">Разверните AdventureWorksDW toosee hello таблицам образца базы данных.</span><span class="sxs-lookup"><span data-stu-id="79760-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Обзор AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="79760-140">2) Запуск пробного запроса</span><span class="sxs-lookup"><span data-stu-id="79760-140">2. Run a sample query</span></span>
<span data-ttu-id="79760-141">Теперь, когда соединение было tooyour установленной базы данных, давайте написать запрос.</span><span class="sxs-lookup"><span data-stu-id="79760-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="79760-142">Щелкните правой кнопкой мыши базу данных в обозревателе объектов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="79760-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="79760-143">Выберите пункт **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="79760-143">Select **New Query**.</span></span> <span data-ttu-id="79760-144">Откроется окно нового запроса.</span><span class="sxs-lookup"><span data-stu-id="79760-144">A new query window opens.</span></span>
   
    ![Создать запрос][5]
3. <span data-ttu-id="79760-146">Скопируйте этот запрос TSQL в окно запроса hello:</span><span class="sxs-lookup"><span data-stu-id="79760-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="79760-147">Выполните запрос hello.</span><span class="sxs-lookup"><span data-stu-id="79760-147">Run hello query.</span></span> <span data-ttu-id="79760-148">toodo это, нажмите кнопку со стрелкой hello зеленый или использовать следующие сочетания hello: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="79760-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Выполнение запроса][6]
5. <span data-ttu-id="79760-150">Взгляните на результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="79760-150">Look at hello query results.</span></span> <span data-ttu-id="79760-151">В этом примере таблицы FactInternetSales hello содержит 60398 строк.</span><span class="sxs-lookup"><span data-stu-id="79760-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Результаты запроса][7]

## <a name="next-steps"></a><span data-ttu-id="79760-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79760-153">Next steps</span></span>
<span data-ttu-id="79760-154">Теперь, когда вы сможете подключиться и запросов, попробуйте [визуализация данных hello с PowerBI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="79760-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="79760-155">tooconfigure среды для проверки подлинности Azure Active Directory, в разделе [tooSQL хранилища данных проверки подлинности][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="79760-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
