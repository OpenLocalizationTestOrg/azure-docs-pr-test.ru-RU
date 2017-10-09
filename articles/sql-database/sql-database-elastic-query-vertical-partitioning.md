---
title: "aaaQuery в облаке баз данных с разными схемами | Документы Microsoft"
description: "как tooset копирование межбазовые запросы по вертикальной секции"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="f1c64-103">Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f1c64-103">Query across cloud databases with different schemas (preview)</span></span>
![Запросы между таблицами в разных базах данных][1]

<span data-ttu-id="f1c64-105">Базы данных с вертикальным секционированием используют разные наборы таблиц в разных базах данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="f1c64-106">Это означает, что в этой схеме hello отличается на разных базах данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="f1c64-107">Например, все таблицы, связанные с данными инвентаризации, хранятся в одной базе данных, а таблицы, связанные с учетом, — в другой.</span><span class="sxs-lookup"><span data-stu-id="f1c64-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f1c64-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1c64-108">Prerequisites</span></span>
* <span data-ttu-id="f1c64-109">Hello пользователь должен обладать разрешением ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="f1c64-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="f1c64-110">Это разрешение входит в состав hello разрешение ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="f1c64-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="f1c64-111">Разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые toorefer toohello базового источника данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="f1c64-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="f1c64-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="f1c64-113">В отличие от с горизонтального секционирования этих инструкций DDL не полагаться на определение уровня данных с карты сегментов через клиентскую библиотеку hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="f1c64-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="f1c64-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="f1c64-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="f1c64-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="f1c64-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="f1c64-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="f1c64-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="f1c64-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="f1c64-118">Создание главного ключа и учетных данных для конкретной базы данных</span><span class="sxs-lookup"><span data-stu-id="f1c64-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="f1c64-119">Hello учетных данных используется hello эластичной запроса tooconnect tooyour удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="f1c64-120">Убедитесь, что hello `<username>` не должно содержать **»@servername»** суффикс.</span><span class="sxs-lookup"><span data-stu-id="f1c64-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="f1c64-121">Создание внешних источников данных</span><span class="sxs-lookup"><span data-stu-id="f1c64-121">Create external data sources</span></span>
<span data-ttu-id="f1c64-122">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="f1c64-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="f1c64-123">необходимо задать параметр ТИПА Hello слишком**реляционной СУБД**.</span><span class="sxs-lookup"><span data-stu-id="f1c64-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="f1c64-124">Пример</span><span class="sxs-lookup"><span data-stu-id="f1c64-124">Example</span></span>
<span data-ttu-id="f1c64-125">Hello следующий пример иллюстрирует использование hello hello инструкции CREATE для внешних источников данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="f1c64-126">Список hello tooretrieve текущего внешних источников данных:</span><span class="sxs-lookup"><span data-stu-id="f1c64-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="f1c64-127">Внешние таблицы</span><span class="sxs-lookup"><span data-stu-id="f1c64-127">External Tables</span></span>
<span data-ttu-id="f1c64-128">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="f1c64-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="f1c64-129">Пример</span><span class="sxs-lookup"><span data-stu-id="f1c64-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="f1c64-130">Привет, в следующем примере показано, как tooretrieve hello список внешних таблиц из текущей базы данных hello:</span><span class="sxs-lookup"><span data-stu-id="f1c64-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="f1c64-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="f1c64-131">Remarks</span></span>
<span data-ttu-id="f1c64-132">Эластичный запрос расширяет hello существующей внешней таблицы синтаксис toodefine внешних таблиц, использующих внешним источникам данных типа реляционной СУБД.</span><span class="sxs-lookup"><span data-stu-id="f1c64-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="f1c64-133">Определение внешней таблицы для вертикального секционирования рассматриваются следующие аспекты hello:</span><span class="sxs-lookup"><span data-stu-id="f1c64-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="f1c64-134">**Схемы**: hello внешней таблицы DDL определяет схему, можно использовать в запросах.</span><span class="sxs-lookup"><span data-stu-id="f1c64-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="f1c64-135">Hello схемы, предоставленных в определении внешней таблицы должен toomatch hello схемы таблиц hello в hello удаленной базы данных, где хранится hello фактические данные.</span><span class="sxs-lookup"><span data-stu-id="f1c64-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="f1c64-136">**Ссылка на удаленную базу данных**: hello внешней таблицы DDL ссылается tooan внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="f1c64-137">Hello внешнего источника данных указывает имя логического сервера hello и имя базы данных hello удаленной базы данных, где хранятся данные таблицы фактических hello.</span><span class="sxs-lookup"><span data-stu-id="f1c64-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="f1c64-138">С помощью внешнего источника данных, как показано в предыдущем разделе hello, hello синтаксис toocreate внешних таблиц выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f1c64-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="f1c64-139">предложение источник_данных Hello определяет hello внешнего источника данных (т. е. hello удаленной базы данных в случае вертикальное секционирование), используемый для hello внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="f1c64-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="f1c64-140">предложения SCHEMA_NAME и OBJECT_NAME Hello содержат hello возможность toomap hello внешней таблицы определение tooa таблицы в другую схему hello удаленной базы данных или таблицы tooa с другим именем, соответственно.</span><span class="sxs-lookup"><span data-stu-id="f1c64-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="f1c64-141">Это полезно, если требуется toodefine представление каталога tooa внешней таблицы или динамического административного Представления в удаленной базе данных - или другая ситуация, где имя удаленной таблицы hello уже занято локально.</span><span class="sxs-lookup"><span data-stu-id="f1c64-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="f1c64-142">Hello следующая инструкция DDL удаляет существующее определение внешней таблицы из локального каталога hello.</span><span class="sxs-lookup"><span data-stu-id="f1c64-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="f1c64-143">Он не влияет на hello удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="f1c64-144">**Разрешения для ВНЕШНЕЙ таблицы в инструкции CREATE, DROP**: для внешней таблицы DDL, который также требуется toorefer toohello базового источника данных, необходимы разрешения ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="f1c64-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="f1c64-145">Вопросы безопасности</span><span class="sxs-lookup"><span data-stu-id="f1c64-145">Security considerations</span></span>
<span data-ttu-id="f1c64-146">Пользователи с доступом toohello внешней таблицы автоматически получают доступ toohello удаленные базовые таблицы под hello учетных данных, заданный в определении источника внешних данных hello.</span><span class="sxs-lookup"><span data-stu-id="f1c64-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="f1c64-147">Следует тщательно управлять доступом toohello внешней таблицы в порядке tooavoid нежелательные повышение привилегий через hello учетных данных источника внешних данных hello.</span><span class="sxs-lookup"><span data-stu-id="f1c64-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="f1c64-148">Регулярные разрешения SQL может быть используется tooGRANT или REVOKE доступа tooan внешней таблицы, как если бы он был обычной таблицы.</span><span class="sxs-lookup"><span data-stu-id="f1c64-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="f1c64-149">Пример: запрос баз данных с вертикальным секционированием</span><span class="sxs-lookup"><span data-stu-id="f1c64-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="f1c64-150">Hello следующий запрос выполняет Тройное соединение между hello двух локальных таблиц заказов и порядок строк и hello удаленной таблицы для клиентов.</span><span class="sxs-lookup"><span data-stu-id="f1c64-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="f1c64-151">Ниже приведен пример hello ссылку данных сценария для эластичного запроса:</span><span class="sxs-lookup"><span data-stu-id="f1c64-151">This is an example of hello reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="f1c64-152">Хранимая процедура для удаленного выполнения T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="f1c64-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="f1c64-153">Эластичный запроса также представляет хранимую процедуру, которая обеспечивает прямой доступ toohello сегментов.</span><span class="sxs-lookup"><span data-stu-id="f1c64-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="f1c64-154">Hello вызывается хранимая процедура [sp\_выполнение \_удаленного](https://msdn.microsoft.com/library/mt703714) и может быть используется tooexecute удаленных хранимых процедур или код T-SQL на hello удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="f1c64-155">Он принимает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f1c64-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="f1c64-156">Имя источника данных (nvarchar): имя hello hello внешнего источника данных типа реляционной СУБД.</span><span class="sxs-lookup"><span data-stu-id="f1c64-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="f1c64-157">Запрос (nvarchar): hello T-SQL запрос toobe выполнена на каждый сегмент.</span><span class="sxs-lookup"><span data-stu-id="f1c64-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="f1c64-158">Объявление параметра (nvarchar) - необязательно: строка, в которой определения типов данных для параметров hello в качестве параметра запроса hello (например sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="f1c64-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="f1c64-159">Список значений параметров (необязательно): разделенный запятыми список значений параметров (например, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="f1c64-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="f1c64-160">Hello sp\_выполнение\_удаленного использует hello внешнего источника данных в hello параметров вызова tooexecute hello, вводимых в удаленных базах данных hello инструкции T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f1c64-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="f1c64-161">Она использует учетные данные hello hello внешних данных tooconnect toohello shardmap диспетчера базы данных-источника и hello удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="f1c64-162">Пример:</span><span class="sxs-lookup"><span data-stu-id="f1c64-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="f1c64-163">Подключение для инструментов</span><span class="sxs-lookup"><span data-stu-id="f1c64-163">Connectivity for tools</span></span>
<span data-ttu-id="f1c64-164">Можно использовать регулярные tooconnect строки подключения SQL Server восстановления toodatabases средств интеграции бизнес-Аналитики и данных на сервере баз данных SQL Server hello эластичной запросов включена и внешних таблиц, определенных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="f1c64-165">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f1c64-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="f1c64-166">Затем можно ссылаться toohello эластичной запрос к базе данных и ее внешней таблицы, так же, как и другие базы данных SQL Server, что для подключения toowith средством.</span><span class="sxs-lookup"><span data-stu-id="f1c64-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="f1c64-167">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="f1c64-167">Best practices</span></span>
* <span data-ttu-id="f1c64-168">Убедитесь, что в этой базе данных hello эластичной запроса конечной точки задано удаленной базы данных toohello доступ путем разрешения доступа для служб Azure в конфигурации брандмауэра баз данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f1c64-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="f1c64-169">Эти учетные данные hello также убедиться, указанное во внешних данных hello определение источника успешно входят в удаленной базе данных hello и имеет hello разрешения tooaccess hello удаленной таблицы.</span><span class="sxs-lookup"><span data-stu-id="f1c64-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="f1c64-170">Эластичный запроса оптимально подходит для запросов где большинство hello вычисление может выполняться на hello удаленных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="f1c64-171">Как правило, получается hello наилучшую производительность запросов с предикатами Выборочный фильтров, которые могут быть обработаны на hello удаленных баз данных или соединения, которые могут быть полностью выполнены hello удаленную базу данных.</span><span class="sxs-lookup"><span data-stu-id="f1c64-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="f1c64-172">Другие шаблоны запросов может потребоваться tooload большие объемы данных из удаленной базы данных hello и может наблюдаться снижение производительности.</span><span class="sxs-lookup"><span data-stu-id="f1c64-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f1c64-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f1c64-173">Next steps</span></span>

* <span data-ttu-id="f1c64-174">Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1c64-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="f1c64-175">Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="f1c64-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="f1c64-176">Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f1c64-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="f1c64-177">Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="f1c64-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="f1c64-178">В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.</span><span class="sxs-lookup"><span data-stu-id="f1c64-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
