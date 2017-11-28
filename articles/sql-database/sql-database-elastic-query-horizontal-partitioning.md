---
title: "Отчеты по масштабируемым облачным базам данных | Документация Майкрософт"
description: "настройка эластичных запросов при горизонтальном секционировании"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 62b5bcd26aa1ed219fb38970916e0e8847ceb577
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="be7b1-103">Отчеты по масштабируемым облачным базам данных (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="be7b1-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Запрос по сегментам][1]

<span data-ttu-id="be7b1-105">Сегментированные базы данных распределяют строки по масштабируемому уровню данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="be7b1-106">Во всех базах данных секционирования используется одна и та же схема — это называется горизонтальным секционированием.</span><span class="sxs-lookup"><span data-stu-id="be7b1-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="be7b1-107">Используя эластичный запрос, можно создавать отчеты, охватывающие все базы данных в сегментированной базе данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="be7b1-108">Чтобы быстро приступить к работе, ознакомьтесь со статьей [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="be7b1-109">Сведения для несегментированных баз данных см. в статье [Запрос к нескольким облачным базам данных с разными схемами](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="be7b1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be7b1-110">Prerequisites</span></span>
* <span data-ttu-id="be7b1-111">Создайте карту сегментов с помощью клиентской библиотеки эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="be7b1-112">Ознакомьтесь с [управлением картами сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="be7b1-113">Можно также использовать пример приложения в статье [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="be7b1-114">Кроме того, можно ознакомиться с разделом [Перенос существующих баз данных для масштабирования](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="be7b1-115">Пользователь должен иметь разрешение ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="be7b1-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="be7b1-116">Это разрешение включено в разрешение ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="be7b1-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="be7b1-117">Для обращения к базовому источнику данных необходимы разрешения ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="be7b1-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="be7b1-118">Обзор</span><span class="sxs-lookup"><span data-stu-id="be7b1-118">Overview</span></span>
<span data-ttu-id="be7b1-119">Эти инструкции позволяют представлять метаданные уровня сегментированных данных через запрос к эластичной базе данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="be7b1-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="be7b1-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="be7b1-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="be7b1-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="be7b1-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="be7b1-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="be7b1-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="be7b1-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="be7b1-124">1.1. Создание главного ключа и учетных данных для конкретной базы данных</span><span class="sxs-lookup"><span data-stu-id="be7b1-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="be7b1-125">Учетные данные используются эластичным запросом для подключения к удаленным базам данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="be7b1-126">Убедитесь, что значение *\<username\>* не содержит суффикс *@servername*.</span><span class="sxs-lookup"><span data-stu-id="be7b1-126">Make sure that the *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="be7b1-127">1.2. Создание внешних источников данных</span><span class="sxs-lookup"><span data-stu-id="be7b1-127">1.2 Create external data sources</span></span>
<span data-ttu-id="be7b1-128">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="be7b1-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="be7b1-129">Пример</span><span class="sxs-lookup"><span data-stu-id="be7b1-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="be7b1-130">Получение списка актуальных внешних источников данных:</span><span class="sxs-lookup"><span data-stu-id="be7b1-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="be7b1-131">Внешний источник данных ссылается на вашу карту сегментов.</span><span class="sxs-lookup"><span data-stu-id="be7b1-131">The external data source references your shard map.</span></span> <span data-ttu-id="be7b1-132">Затем эластичный запрос использует внешний источник данных и соответствующую карту сегментов для перебора баз данных, входящих в уровень данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="be7b1-133">Когда обрабатывается эластичный запрос, для чтения карты сегментов и доступа к данным в сегментах используются одни и те же учетные данные.</span><span class="sxs-lookup"><span data-stu-id="be7b1-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="be7b1-134">1.3. Создание внешних таблиц</span><span class="sxs-lookup"><span data-stu-id="be7b1-134">1.3 Create external tables</span></span>
<span data-ttu-id="be7b1-135">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="be7b1-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="be7b1-136">**Пример**</span><span class="sxs-lookup"><span data-stu-id="be7b1-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="be7b1-137">Получение списка внешних таблиц из текущей базы данных:</span><span class="sxs-lookup"><span data-stu-id="be7b1-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="be7b1-138">Удаление внешних таблиц:</span><span class="sxs-lookup"><span data-stu-id="be7b1-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="be7b1-139">Примечания</span><span class="sxs-lookup"><span data-stu-id="be7b1-139">Remarks</span></span>
<span data-ttu-id="be7b1-140">Предложение DATA\_SOURCE определяет внешний источник данных (карту сегментов) для внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="be7b1-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="be7b1-141">Предложения SCHEMA\_NAME и OBJECT\_NAME сопоставляют определение внешней таблицы с таблицей в другой схеме.</span><span class="sxs-lookup"><span data-stu-id="be7b1-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="be7b1-142">Если эти предложения отсутствуют, то предполагается, что удаленный объект является таблицей «dbo», имя которой совпадает с именем внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="be7b1-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="be7b1-143">Это особенно необходимо, если имя удаленной таблицы уже занято в базе данных, где создается внешняя таблица.</span><span class="sxs-lookup"><span data-stu-id="be7b1-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="be7b1-144">Например, вы хотите определить внешнюю таблицу для получения общего представления из представлений каталогов или динамических административных представлений, которые находятся на вашем развернутом уровне данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="be7b1-145">Так как представления каталогов и динамические административные представления уже существуют локально, их имена нельзя использовать для определения внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="be7b1-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="be7b1-146">Вместо этого вы можете задать другое имя и в предложениях SCHEMA\_NAME и OBJECT\_NAME использовать имя представления каталога или динамического административного представления.</span><span class="sxs-lookup"><span data-stu-id="be7b1-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="be7b1-147">(См. пример ниже.)</span><span class="sxs-lookup"><span data-stu-id="be7b1-147">(See the example below.)</span></span> 

<span data-ttu-id="be7b1-148">Предложение DISTRIBUTION определяет распределение данных, используемое для этой таблицы:</span><span class="sxs-lookup"><span data-stu-id="be7b1-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="be7b1-149">Обработчик запросов использует сведения, указанные в предложении DISTRIBUTION, для создания наиболее эффективных планов запросов.</span><span class="sxs-lookup"><span data-stu-id="be7b1-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="be7b1-150">**SHARDED** означает, что данные секционируются по базе данных горизонтально.</span><span class="sxs-lookup"><span data-stu-id="be7b1-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="be7b1-151">Ключ секционирования для распределения данных указывается в параметре **<sharding_column_name>**.</span><span class="sxs-lookup"><span data-stu-id="be7b1-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="be7b1-152">**REPLICATED** означает, что в каждой базе данных имеются идентичные копии таблицы.</span><span class="sxs-lookup"><span data-stu-id="be7b1-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="be7b1-153">Вы должны самостоятельно позаботиться о соответствии реплик во всех базах данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="be7b1-154">**ROUND\_ROBIN** означает, что таблица секционируется горизонтально с применением метода распределения в зависимости от приложений.</span><span class="sxs-lookup"><span data-stu-id="be7b1-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="be7b1-155">**Ссылка на уровень данных**: язык DDL внешней таблицы ссылается на внешний источник данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="be7b1-156">Во внешнем источнике данных указывается карта сегментов, в которой есть внешняя таблица, содержащая сведения, необходимые для поиска всех баз данных на вашем уровне данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="be7b1-157">Вопросы безопасности</span><span class="sxs-lookup"><span data-stu-id="be7b1-157">Security considerations</span></span>
<span data-ttu-id="be7b1-158">Пользователи, имеющие доступ к внешней таблице, автоматически получают доступ к базовой удаленной таблице с учетными данными, указанными в определении внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="be7b1-159">Старайтесь избегать нежелательного повышения прав с использованием учетных данных для внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="be7b1-160">Методы GRANT или REVOKE применяются к внешней таблице так же, как и к обычной.</span><span class="sxs-lookup"><span data-stu-id="be7b1-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="be7b1-161">Определив внешний источник данных и внешние таблицы, вы можете использовать все возможности T-SQL для создания запросов к внешним таблицам.</span><span class="sxs-lookup"><span data-stu-id="be7b1-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="be7b1-162">Пример: запрос баз данных с горизонтальным секционированием</span><span class="sxs-lookup"><span data-stu-id="be7b1-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="be7b1-163">С помощью следующего запроса устанавливается трехстороннее соединение между хранилищами, заказами и строками заказов, при этом используется несколько статистических выражений и выборочный фильтр.</span><span class="sxs-lookup"><span data-stu-id="be7b1-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="be7b1-164">Здесь предполагается, что используется (1) горизонтальное секционирование (сегментирование) и (2) что сегментирование хранилищ, заказов и строк заказов выполняется по столбцу с идентификатором хранилища. В этом случае эластичный запрос может выровнять соединения в сегментах и параллельно обработать ресурсоемкую часть запроса в сегментах.</span><span class="sxs-lookup"><span data-stu-id="be7b1-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="be7b1-165">Хранимая процедура для удаленного выполнения T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="be7b1-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="be7b1-166">С функцией эластичных запросов вам становится доступна хранимая процедура, которая обеспечивает прямой доступ к сегментам.</span><span class="sxs-lookup"><span data-stu-id="be7b1-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="be7b1-167">Хранимая процедура называется [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714), она может использоваться для выполнения удаленных хранимых процедур или кода T-SQL в удаленных базах данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="be7b1-168">Она принимает следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="be7b1-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="be7b1-169">Имя источника данных (nvarchar): имя внешнего источника данных типа "реляционная СУБД".</span><span class="sxs-lookup"><span data-stu-id="be7b1-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="be7b1-170">Запрос (nvarchar): запрос T-SQL, выполняемый для каждого сегмента.</span><span class="sxs-lookup"><span data-stu-id="be7b1-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="be7b1-171">Объявление параметра (nvarchar, необязательно): строка с определениями типов данных, используемых в параметрах запроса (например, для процедуры sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="be7b1-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="be7b1-172">Список значений параметров (необязательно): разделенный запятыми список значений параметров (например, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="be7b1-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="be7b1-173">Процедура sp\_execute\_remote использует внешний источник данных, указанный в параметрах вызова, для выполнения заданной инструкции T-SQL в удаленных базах данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="be7b1-174">Она использует учетные данные внешнего источника данных для подключения к базе данных диспетчера ShardMap и удаленным базам данных.</span><span class="sxs-lookup"><span data-stu-id="be7b1-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="be7b1-175">Пример:</span><span class="sxs-lookup"><span data-stu-id="be7b1-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="be7b1-176">Подключение для инструментов</span><span class="sxs-lookup"><span data-stu-id="be7b1-176">Connectivity for tools</span></span>
<span data-ttu-id="be7b1-177">Используйте обычные строки подключения SQL Server для подключения вашего приложения, инструментов бизнес-аналитики и интеграции данных к базе данных с определениями внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="be7b1-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="be7b1-178">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="be7b1-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="be7b1-179">Затем добавьте ссылку на запрос к эластичной базе данных, как к любой другой базе данных SQL Server, подключенной к приложению. После этого из своего инструмента или приложения вы сможете использовать внешние таблицы так, как если бы они были локальными таблицами.</span><span class="sxs-lookup"><span data-stu-id="be7b1-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="be7b1-180">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="be7b1-180">Best practices</span></span>
* <span data-ttu-id="be7b1-181">Убедитесь, что брандмауэры баз данных SQL обеспечивают конечной базе данных с эластичными запросами доступ к базе данных карты сегментов и всем сегментам.</span><span class="sxs-lookup"><span data-stu-id="be7b1-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="be7b1-182">Эластичный запрос не предполагает проверку или распределение данных в соответствии с внешней таблицей.</span><span class="sxs-lookup"><span data-stu-id="be7b1-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="be7b1-183">Если фактическое распространение данных отличается от определения таблицы, то результаты запросов могут быть непредсказуемыми.</span><span class="sxs-lookup"><span data-stu-id="be7b1-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="be7b1-184">Функция эластичных запросов в настоящее время не позволяет исключать сегменты, когда предикаты для ключа сегментирования безопасно исключают определенные сегменты из процесса обработки.</span><span class="sxs-lookup"><span data-stu-id="be7b1-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="be7b1-185">Эластичные запросы оптимальны, когда основная часть вычислений может быть выполнена в сегментах.</span><span class="sxs-lookup"><span data-stu-id="be7b1-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="be7b1-186">Обычно наиболее эффективны запросы с предикатами выборочных фильтров, дающие возможность вычисления в сегментах или соединениях путем секционирования ключей с выравниванием по секциям для всех сегментов.</span><span class="sxs-lookup"><span data-stu-id="be7b1-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="be7b1-187">Для других шаблонов запросов может потребоваться загрузка больших объемов данных из сегментов в головной узел, что может стать причиной снижения производительности.</span><span class="sxs-lookup"><span data-stu-id="be7b1-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="be7b1-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be7b1-188">Next steps</span></span>

* <span data-ttu-id="be7b1-189">Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="be7b1-190">Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="be7b1-191">Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="be7b1-192">Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="be7b1-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="be7b1-193">В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.</span><span class="sxs-lookup"><span data-stu-id="be7b1-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
