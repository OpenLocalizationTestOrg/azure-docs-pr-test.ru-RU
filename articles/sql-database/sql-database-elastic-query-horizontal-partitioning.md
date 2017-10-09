---
title: "aaaReporting между базами данных с горизонтальным масштабированием облачных | Документы Microsoft"
description: "как tooset копирование эластичной запросов за горизонтальных секций"
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
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="46eba-103">Отчеты по масштабируемым облачным базам данных (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="46eba-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Запрос по сегментам][1]

<span data-ttu-id="46eba-105">Сегментированные базы данных распределяют строки по масштабируемому уровню данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="46eba-106">Hello схемы похоже на все участвующие базы данных, также известные как горизонтальное секционирование.</span><span class="sxs-lookup"><span data-stu-id="46eba-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="46eba-107">Используя эластичный запрос, можно создавать отчеты, охватывающие все базы данных в сегментированной базе данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="46eba-108">Чтобы быстро приступить к работе, ознакомьтесь со статьей [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="46eba-109">Сведения для несегментированных баз данных см. в статье [Запрос к нескольким облачным базам данных с разными схемами](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="46eba-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="46eba-110">Prerequisites</span></span>
* <span data-ttu-id="46eba-111">Создание карты сегментов с помощью клиентской библиотеки hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="46eba-112">Ознакомьтесь с [управлением картами сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="46eba-113">Или использовать пример приложения hello [начало работы с инструментами эластичной базы данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="46eba-114">Кроме того, в разделе [миграции существующей базы данных вне tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="46eba-115">Hello пользователь должен обладать разрешением ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="46eba-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="46eba-116">Это разрешение входит в состав hello разрешение ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="46eba-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="46eba-117">Разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые toorefer toohello базового источника данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="46eba-118">Обзор</span><span class="sxs-lookup"><span data-stu-id="46eba-118">Overview</span></span>
<span data-ttu-id="46eba-119">Эти инструкции создания представления метаданных hello уровень сегментированных данных в hello эластичной запрос к базе данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="46eba-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="46eba-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="46eba-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="46eba-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="46eba-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="46eba-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="46eba-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="46eba-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="46eba-124">1.1. Создание главного ключа и учетных данных для конкретной базы данных</span><span class="sxs-lookup"><span data-stu-id="46eba-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="46eba-125">Hello учетных данных используется hello эластичной запроса tooconnect tooyour удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="46eba-126">Убедитесь в том, что hello *»\<username\>»* не должно содержать *»@servername»* суффикс.</span><span class="sxs-lookup"><span data-stu-id="46eba-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="46eba-127">1.2. Создание внешних источников данных</span><span class="sxs-lookup"><span data-stu-id="46eba-127">1.2 Create external data sources</span></span>
<span data-ttu-id="46eba-128">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="46eba-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="46eba-129">Пример</span><span class="sxs-lookup"><span data-stu-id="46eba-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="46eba-130">Получение списка hello текущего внешних источников данных:</span><span class="sxs-lookup"><span data-stu-id="46eba-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="46eba-131">Hello внешний источник данных ссылается на карте сегментов.</span><span class="sxs-lookup"><span data-stu-id="46eba-131">hello external data source references your shard map.</span></span> <span data-ttu-id="46eba-132">Запрос эластичной затем использует hello внешнего источника данных и базовой сегментов карты tooenumerate hello баз данных, которые участвуют в уровень данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="46eba-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="46eba-133">Hello же учетные данные, используемые tooread карта сегментов hello и tooaccess hello данные на сегменты hello во время обработки hello эластичной запроса.</span><span class="sxs-lookup"><span data-stu-id="46eba-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="46eba-134">1.3. Создание внешних таблиц</span><span class="sxs-lookup"><span data-stu-id="46eba-134">1.3 Create external tables</span></span>
<span data-ttu-id="46eba-135">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="46eba-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="46eba-136">**Пример**</span><span class="sxs-lookup"><span data-stu-id="46eba-136">**Example**</span></span>

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

<span data-ttu-id="46eba-137">Получить список hello внешние таблицы из текущей базы данных hello:</span><span class="sxs-lookup"><span data-stu-id="46eba-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="46eba-138">toodrop внешних таблиц:</span><span class="sxs-lookup"><span data-stu-id="46eba-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="46eba-139">Примечания</span><span class="sxs-lookup"><span data-stu-id="46eba-139">Remarks</span></span>
<span data-ttu-id="46eba-140">Hello данных\_предложение источника определяет hello внешнего источника данных (карта сегментов), используемый для hello внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="46eba-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="46eba-141">Hello СХЕМЫ\_имя и объект\_предложений имя сопоставления hello таблица tooa определения внешней таблицы в другую схему.</span><span class="sxs-lookup"><span data-stu-id="46eba-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="46eba-142">Если не указано, hello схему удаленного объекта hello полагается toobe «dbo» а его имя является определяемое имя внешней таблицы идентичные toohello toobe.</span><span class="sxs-lookup"><span data-stu-id="46eba-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="46eba-143">Это полезно, если hello имя удаленной таблицы уже используется в базе данных hello место toocreate hello внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="46eba-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="46eba-144">Например требуется toodefine внешней таблицы tooget статистического представления представлений каталога или динамических административных представлений с горизонтальным масштабированием данными уровня.</span><span class="sxs-lookup"><span data-stu-id="46eba-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="46eba-145">Поскольку представления каталогов и динамические административные представления уже существует локально, не может использовать их имена для определения hello внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="46eba-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="46eba-146">Вместо этого используйте другое имя и используйте представление каталога hello или hello имя динамические административные Представления в СХЕМЕ hello\_имя и (или) ОБЪЕКТА\_имя предложения.</span><span class="sxs-lookup"><span data-stu-id="46eba-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="46eba-147">(См. пример hello).</span><span class="sxs-lookup"><span data-stu-id="46eba-147">(See hello example below.)</span></span> 

<span data-ttu-id="46eba-148">предложение РАСПРОСТРАНЕНИЯ Hello указывает hello распределение данных, используемого для этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="46eba-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="46eba-149">Hello обработчик запросов использует сведения hello в hello РАСПРОСТРАНЕНИЯ предложение toobuild hello наиболее эффективный планов запросов.</span><span class="sxs-lookup"><span data-stu-id="46eba-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="46eba-150">**СЕГМЕНТИРОВАННЫХ** означает данные секционируются горизонтально hello базах данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="46eba-151">ключ разделов для распределения данных hello hello Hello **< sharding_column_name >** параметра.</span><span class="sxs-lookup"><span data-stu-id="46eba-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="46eba-152">**РЕПЛИКАЦИЯ** означает, что одинаковых копий hello таблицы присутствуют в каждой базе данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="46eba-153">Это ваш tooensure ответственность, что реплик hello идентичны для всех баз данных hello.</span><span class="sxs-lookup"><span data-stu-id="46eba-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="46eba-154">**ROUND\_ПЕРЕБОРОМ** означает, что hello таблица секционирована по горизонтали с помощью метода распространения зависит от приложения.</span><span class="sxs-lookup"><span data-stu-id="46eba-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="46eba-155">**Ссылка на уровень данных**: hello внешней таблицы DDL ссылается tooan внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="46eba-156">Hello внешнего источника данных указывает карта сегментов, предоставляющий hello внешней таблицы toolocate необходимые сведения hello всех hello базах данных уровня данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="46eba-157">Вопросы безопасности</span><span class="sxs-lookup"><span data-stu-id="46eba-157">Security considerations</span></span>
<span data-ttu-id="46eba-158">Пользователи с доступом toohello внешней таблицы автоматически получают доступ toohello удаленные базовые таблицы под hello учетных данных, заданный в определении источника внешних данных hello.</span><span class="sxs-lookup"><span data-stu-id="46eba-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="46eba-159">Избегайте нежелательных повышение привилегий через учетных данных hello hello внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="46eba-160">Методы GRANT или REVOKE применяются к внешней таблице так же, как и к обычной.</span><span class="sxs-lookup"><span data-stu-id="46eba-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="46eba-161">Определив внешний источник данных и внешние таблицы, вы можете использовать все возможности T-SQL для создания запросов к внешним таблицам.</span><span class="sxs-lookup"><span data-stu-id="46eba-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="46eba-162">Пример: запрос баз данных с горизонтальным секционированием</span><span class="sxs-lookup"><span data-stu-id="46eba-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="46eba-163">Hello следующий запрос выполняет Тройное соединение между хранилищами, заказов и строк заказов и использует несколько статистических выражений и выборочной фильтра.</span><span class="sxs-lookup"><span data-stu-id="46eba-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="46eba-164">Предполагается, что (1) горизонтальных секционирования (сегментов) и (2) порядок строк, заказов и хранилищ сегментированных по столбцу идентификатора hello хранилища, и hello эластичной запроса можно выравнивать hello соединения на сегменты hello и обрабатывать hello ресурсоемким hello запроса hello сегменты в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="46eba-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="46eba-165">Хранимая процедура для удаленного выполнения T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="46eba-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="46eba-166">Эластичный запроса также представляет хранимую процедуру, которая обеспечивает прямой доступ toohello сегментов.</span><span class="sxs-lookup"><span data-stu-id="46eba-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="46eba-167">Hello вызывается хранимая процедура [sp\_выполнение \_удаленного](https://msdn.microsoft.com/library/mt703714) и может быть используется tooexecute удаленных хранимых процедур или код T-SQL на hello удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="46eba-168">Он принимает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="46eba-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="46eba-169">Имя источника данных (nvarchar): имя hello hello внешнего источника данных типа реляционной СУБД.</span><span class="sxs-lookup"><span data-stu-id="46eba-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="46eba-170">Запрос (nvarchar): hello T-SQL запрос toobe выполнена на каждый сегмент.</span><span class="sxs-lookup"><span data-stu-id="46eba-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="46eba-171">Объявление параметра (nvarchar) - необязательно: строка, в которой определения типов данных для параметров hello в качестве параметра запроса hello (например sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="46eba-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="46eba-172">Список значений параметров (необязательно): разделенный запятыми список значений параметров (например, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="46eba-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="46eba-173">Hello sp\_выполнение\_удаленного использует hello внешнего источника данных в hello параметров вызова tooexecute hello, вводимых в удаленных базах данных hello инструкции T-SQL.</span><span class="sxs-lookup"><span data-stu-id="46eba-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="46eba-174">Она использует учетные данные hello hello внешних данных tooconnect toohello shardmap диспетчера базы данных-источника и hello удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="46eba-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="46eba-175">Пример:</span><span class="sxs-lookup"><span data-stu-id="46eba-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="46eba-176">Подключение для инструментов</span><span class="sxs-lookup"><span data-stu-id="46eba-176">Connectivity for tools</span></span>
<span data-ttu-id="46eba-177">Использовать регулярные tooconnect строки подключения SQL Server приложения, бизнес-Аналитики и данных интеграции средств toohello базы данных с определениях внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="46eba-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="46eba-178">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="46eba-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="46eba-179">Ссылаться на базу данных hello эластичной запросов, как и любой другой SQL Server базы данных, соединение toohello инструмент и использовать внешние таблицы из средства или приложения, как если бы они были локальными таблицами.</span><span class="sxs-lookup"><span data-stu-id="46eba-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="46eba-180">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="46eba-180">Best practices</span></span>
* <span data-ttu-id="46eba-181">Убедитесь, что для этой базы данных hello эластичной запроса конечной точки предоставлен доступ к базе данных shardmap toohello и все сегменты через брандмауэры SQL DB приветствия.</span><span class="sxs-lookup"><span data-stu-id="46eba-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="46eba-182">Проверяет, или применять hello распределение данных, определяемый hello внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="46eba-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="46eba-183">При распространении фактических данных отличается от распространения hello, указанный в определении таблицы, запросы, может привести к непредвиденным результатам.</span><span class="sxs-lookup"><span data-stu-id="46eba-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="46eba-184">Эластичный запрос в настоящее время не выполняет сегментов исключения при предикаты для ключа сегментирования hello позволяющих toosafely исключения определенных сегментов из обработки.</span><span class="sxs-lookup"><span data-stu-id="46eba-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="46eba-185">Эластичный запроса лучше всего работает для запросов, где большинство hello вычисление может выполняться на сегменты hello.</span><span class="sxs-lookup"><span data-stu-id="46eba-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="46eba-186">Как правило, получается hello наилучшую производительность запросов с предикатами Выборочный фильтров, которые можно оценить на сегменты hello или соединения через hello секционирование ключи, которые могут выполняться в виде выровненные по секциям на всех сегментах.</span><span class="sxs-lookup"><span data-stu-id="46eba-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="46eba-187">Другие шаблоны запросов, может потребоваться tooload большие объемы данных из головного узла hello сегментов toohello и может наблюдаться снижение производительности</span><span class="sxs-lookup"><span data-stu-id="46eba-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="46eba-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46eba-188">Next steps</span></span>

* <span data-ttu-id="46eba-189">Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="46eba-190">Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="46eba-191">Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="46eba-192">Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="46eba-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="46eba-193">В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.</span><span class="sxs-lookup"><span data-stu-id="46eba-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
