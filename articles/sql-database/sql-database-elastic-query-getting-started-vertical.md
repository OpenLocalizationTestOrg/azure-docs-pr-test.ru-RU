---
title: "aaaGet работы с межбазовые запросы (вертикальное секционирование) | Документы Microsoft"
description: "как запрос toouse эластичной базы данных с вертикальное секционирование баз данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="949a5-103">Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="949a5-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="949a5-104">Запрос эластичной базы данных (Предварительная версия) для базы данных SQL Azure позволяет toorun запросов T-SQL, которые охватывают несколько баз данных с помощью одна точка подключения.</span><span class="sxs-lookup"><span data-stu-id="949a5-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="949a5-105">В этом разделе также применяется[вертикальное секционирование баз данных](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="949a5-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="949a5-106">После завершения вы будете: Узнайте, как tooconfigure и использования базы данных SQL Azure tooperform запрос, охватывающих несколько связанных баз данных.</span><span class="sxs-lookup"><span data-stu-id="949a5-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="949a5-107">Дополнительные сведения о функции запросов hello эластичной базы данных см. в разделе [Обзор запросов базы данных SQL Azure эластичной базы данных](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="949a5-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="949a5-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="949a5-108">Prerequisites</span></span>

<span data-ttu-id="949a5-109">Требуется наличие разрешения ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="949a5-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="949a5-110">Это разрешение входит в состав hello разрешение ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="949a5-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="949a5-111">Разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые toorefer toohello базового источника данных.</span><span class="sxs-lookup"><span data-stu-id="949a5-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="949a5-112">Создать hello образцы баз данных</span><span class="sxs-lookup"><span data-stu-id="949a5-112">Create hello sample databases</span></span>
<span data-ttu-id="949a5-113">toostart с необходимы две базы данных toocreate **клиентов** и **заказов**, Здравствуйте, либо в одной или разных логических серверов.</span><span class="sxs-lookup"><span data-stu-id="949a5-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="949a5-114">Выполните следующие запросы на hello hello **заказов** hello toocreate базы данных **OrderInformation** таблицы и ввода данных образец hello.</span><span class="sxs-lookup"><span data-stu-id="949a5-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="949a5-115">Теперь, можно выполнить следующий запрос на hello **клиентов** hello toocreate базы данных **сведения о клиенте** таблицы и ввода данных образец hello.</span><span class="sxs-lookup"><span data-stu-id="949a5-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="949a5-116">Создание объектов базы данных</span><span class="sxs-lookup"><span data-stu-id="949a5-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="949a5-117">Главный ключ и учетные данные для конкретной базы данных</span><span class="sxs-lookup"><span data-stu-id="949a5-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="949a5-118">Откройте SQL Server Management Studio или SQL Server Data Tools в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="949a5-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="949a5-119">Подключения базы данных Orders toohello и выполните следующие команды T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="949a5-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="949a5-120">Hello «username» и «password» должно быть hello имя пользователя и пароль, используемые toologin в базу данных клиентам hello.</span><span class="sxs-lookup"><span data-stu-id="949a5-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="949a5-121">Проверка подлинности с помощью Azure Active Directory и эластичных запросов сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="949a5-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="949a5-122">Внешние источники данных</span><span class="sxs-lookup"><span data-stu-id="949a5-122">External data sources</span></span>
<span data-ttu-id="949a5-123">toocreate внешнего источника данных, выполните следующую команду в базе данных заказов hello hello:</span><span class="sxs-lookup"><span data-stu-id="949a5-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="949a5-124">Внешние таблицы</span><span class="sxs-lookup"><span data-stu-id="949a5-124">External tables</span></span>
<span data-ttu-id="949a5-125">Создайте внешнюю таблицу Orders hello базе данных, который соответствует hello определение таблицы hello сведения о клиенте:</span><span class="sxs-lookup"><span data-stu-id="949a5-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="949a5-126">Выполнение запроса T-SQL к примеру эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="949a5-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="949a5-127">После определения источника внешних данных и внешних таблиц теперь можно использовать tooquery T-SQL внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="949a5-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="949a5-128">Выполните следующий запрос в базе данных заказов hello:</span><span class="sxs-lookup"><span data-stu-id="949a5-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="949a5-129">Стоимость</span><span class="sxs-lookup"><span data-stu-id="949a5-129">Cost</span></span>
<span data-ttu-id="949a5-130">В настоящее время функция запроса hello эластичной базы данных включена в стоимость hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="949a5-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="949a5-131">Сведения о ценах см. на [странице с ценами на базы данных SQL](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="949a5-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="949a5-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="949a5-132">Next steps</span></span>

* <span data-ttu-id="949a5-133">Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="949a5-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="949a5-134">Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="949a5-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="949a5-135">Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="949a5-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="949a5-136">Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="949a5-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="949a5-137">В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.</span><span class="sxs-lookup"><span data-stu-id="949a5-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>