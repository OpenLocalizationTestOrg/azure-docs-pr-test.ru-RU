---
title: "Запрос к нескольким облачным базам данных с разными схемами | Документация Майкрософт"
description: "настройка межбазовых запросов для вертикального секционирования"
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
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="6531a-103">Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="6531a-103">Query across cloud databases with different schemas (preview)</span></span>
![Запросы между таблицами в разных базах данных][1]

<span data-ttu-id="6531a-105">Базы данных с вертикальным секционированием используют разные наборы таблиц в разных базах данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="6531a-106">Это означает, что схемы разных баз данных различаются.</span><span class="sxs-lookup"><span data-stu-id="6531a-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="6531a-107">Например, все таблицы, связанные с данными инвентаризации, хранятся в одной базе данных, а таблицы, связанные с учетом, — в другой.</span><span class="sxs-lookup"><span data-stu-id="6531a-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6531a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6531a-108">Prerequisites</span></span>
* <span data-ttu-id="6531a-109">Пользователь должен иметь разрешение ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="6531a-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="6531a-110">Это разрешение включено в разрешение ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="6531a-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="6531a-111">Для обращения к базовому источнику данных необходимы разрешения ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="6531a-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="6531a-112">Обзор</span><span class="sxs-lookup"><span data-stu-id="6531a-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="6531a-113">В отличие от горизонтального секционирования эти инструкции DDL не зависят от определения уровня данных с помощью карты сегментов через клиентскую библиотеку эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="6531a-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="6531a-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="6531a-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="6531a-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="6531a-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="6531a-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="6531a-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="6531a-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="6531a-118">Создание главного ключа и учетных данных для конкретной базы данных</span><span class="sxs-lookup"><span data-stu-id="6531a-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="6531a-119">Учетные данные используются эластичным запросом для подключения к удаленным базам данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="6531a-120">Убедитесь, что значение `<username>` не содержит суффикс **@servername**.</span><span class="sxs-lookup"><span data-stu-id="6531a-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="6531a-121">Создание внешних источников данных</span><span class="sxs-lookup"><span data-stu-id="6531a-121">Create external data sources</span></span>
<span data-ttu-id="6531a-122">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="6531a-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="6531a-123">Параметру TYPE должно быть присвоено значение **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="6531a-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="6531a-124">Пример</span><span class="sxs-lookup"><span data-stu-id="6531a-124">Example</span></span>
<span data-ttu-id="6531a-125">В следующем примере демонстрируется использование инструкции CREATE для внешних источников данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="6531a-126">Получение списка актуальных внешних источников данных</span><span class="sxs-lookup"><span data-stu-id="6531a-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="6531a-127">Внешние таблицы</span><span class="sxs-lookup"><span data-stu-id="6531a-127">External Tables</span></span>
<span data-ttu-id="6531a-128">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="6531a-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="6531a-129">Пример</span><span class="sxs-lookup"><span data-stu-id="6531a-129">Example</span></span>
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

<span data-ttu-id="6531a-130">В следующем примере показано получение списка внешних таблиц из текущей базы данных:</span><span class="sxs-lookup"><span data-stu-id="6531a-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="6531a-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="6531a-131">Remarks</span></span>
<span data-ttu-id="6531a-132">Эластичные запросы расширяют существующий синтаксис доступа к внешним таблицам, позволяя определять внешние таблицы, использующие внешние источники данных типа реляционной СУБД.</span><span class="sxs-lookup"><span data-stu-id="6531a-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="6531a-133">Определение внешней таблицы для вертикального секционирования содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="6531a-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="6531a-134">**Схема**: язык DDL внешней таблицы определяет схему, которую можно использовать в запросах.</span><span class="sxs-lookup"><span data-stu-id="6531a-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="6531a-135">Схема из определения вашей внешней таблицы должна соответствовать схеме таблиц в удаленной базе данных, в которой хранятся данные.</span><span class="sxs-lookup"><span data-stu-id="6531a-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="6531a-136">**Ссылка на удаленную базу данных**: язык DDL внешней таблицы ссылается на внешний источник данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="6531a-137">Внешний источник данных указывает логическое имя сервера и имя удаленной базы данных, в которой фактически хранятся данные из таблицы.</span><span class="sxs-lookup"><span data-stu-id="6531a-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="6531a-138">Используя внешний источник данных (в соответствии с инструкциями, приведенными в предыдущем разделе), вы можете создавать внешние таблицы при помощи следующего синтаксиса:</span><span class="sxs-lookup"><span data-stu-id="6531a-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="6531a-139">Предложение DATA_SOURCE определяет внешний источник данных (в случае вертикального секционирования это удаленная база данных), используемый для внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="6531a-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="6531a-140">Предложения SCHEMA_NAME и OBJECT_NAME позволяют сопоставить определение внешней таблицы с таблицей из другой схемы в удаленной базе данных или таблицей с другим именем.</span><span class="sxs-lookup"><span data-stu-id="6531a-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="6531a-141">Это удобно, если вы хотите связать внешнюю таблицу с представлением каталога или динамическим административным представлением вашей удаленной базы данных, а также в любой ситуации, в которой имя удаленной таблицы уже локально занято.</span><span class="sxs-lookup"><span data-stu-id="6531a-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="6531a-142">Следующая инструкция DDL удаляет существующее определение внешней таблицы из локального каталога.</span><span class="sxs-lookup"><span data-stu-id="6531a-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="6531a-143">Эта операция не влияет на удаленную базу данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="6531a-144">**Разрешения для инструкции CREATE/DROP EXTERNAL TABLE**: для схемы данных внешней таблицы требуются разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые также для ссылки на базовый источник данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="6531a-145">Вопросы безопасности</span><span class="sxs-lookup"><span data-stu-id="6531a-145">Security considerations</span></span>
<span data-ttu-id="6531a-146">Пользователи, имеющие доступ к внешней таблице, автоматически получают доступ к базовой удаленной таблице с учетными данными, указанными в определении внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="6531a-147">Вам следует тщательно следить за доступом к внешним таблицам во избежание нежелательного повышения привилегий при использовании учетных данных внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="6531a-148">Для предоставления и отмены доступа к внешней таблице используются разрешения SQL, применимые к обычным таблицам.</span><span class="sxs-lookup"><span data-stu-id="6531a-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="6531a-149">Пример: запрос баз данных с вертикальным секционированием</span><span class="sxs-lookup"><span data-stu-id="6531a-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="6531a-150">Следующий запрос выполняет трехстороннее соединение между двумя локальными таблицами заказов и строк заказов с удаленной таблицей клиентов.</span><span class="sxs-lookup"><span data-stu-id="6531a-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="6531a-151">Ниже приведен пример варианта использования ссылочных данных в эластичном запросе:</span><span class="sxs-lookup"><span data-stu-id="6531a-151">This is an example of the reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="6531a-152">Хранимая процедура для удаленного выполнения T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="6531a-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="6531a-153">С функцией эластичных запросов вам становится доступна хранимая процедура, которая обеспечивает прямой доступ к сегментам.</span><span class="sxs-lookup"><span data-stu-id="6531a-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="6531a-154">Хранимая процедура называется [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714), она может использоваться для выполнения удаленных хранимых процедур или кода T-SQL в удаленных базах данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="6531a-155">Она принимает следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="6531a-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="6531a-156">Имя источника данных (nvarchar): имя внешнего источника данных типа "реляционная СУБД".</span><span class="sxs-lookup"><span data-stu-id="6531a-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="6531a-157">Запрос (nvarchar): запрос T-SQL, выполняемый для каждого сегмента.</span><span class="sxs-lookup"><span data-stu-id="6531a-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="6531a-158">Объявление параметра (nvarchar, необязательно): строка с определениями типов данных, используемых в параметрах запроса (например, для процедуры sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="6531a-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="6531a-159">Список значений параметров (необязательно): разделенный запятыми список значений параметров (например, sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="6531a-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="6531a-160">Процедура sp\_execute\_remote использует внешний источник данных, указанный в параметрах вызова, для выполнения заданной инструкции T-SQL в удаленных базах данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="6531a-161">Она использует учетные данные внешнего источника данных для подключения к базе данных диспетчера ShardMap и удаленным базам данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="6531a-162">Пример:</span><span class="sxs-lookup"><span data-stu-id="6531a-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="6531a-163">Подключение для инструментов</span><span class="sxs-lookup"><span data-stu-id="6531a-163">Connectivity for tools</span></span>
<span data-ttu-id="6531a-164">Используйте обычные строки подключения SQL Server для подключения ваших инструментов бизнес-аналитики и средств интеграции данных к серверу баз данных SQL, где включены эластичные запросы и определены внешние таблицы.</span><span class="sxs-lookup"><span data-stu-id="6531a-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="6531a-165">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6531a-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="6531a-166">Затем добавьте ссылку на эластичную базу данных запросов и ее внешние таблицы так же, как и ссылку на любую другую базу данных SQL Server, к которой вы подключались бы с помощью своего средства.</span><span class="sxs-lookup"><span data-stu-id="6531a-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="6531a-167">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="6531a-167">Best practices</span></span>
* <span data-ttu-id="6531a-168">Убедитесь, что эластичный запрос к конечной базе данных имеет доступ к удаленной базе данных. Для этого откройте доступ для служб Azure в конфигурации брандмауэра базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6531a-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="6531a-169">Кроме того, убедитесь, что учетные данные, указанные в определении внешнего источника данных, позволяют войти в удаленную базу данных и имеют разрешения на доступ к удаленной таблице.</span><span class="sxs-lookup"><span data-stu-id="6531a-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="6531a-170">Эластичные запросы оптимальны, когда основная часть вычислений может быть выполнена в удаленной базе данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="6531a-171">Обычно наиболее эффективны запросы с предикатами выборочных фильтров, дающие возможность вычисления в удаленных базах данных, или соединениями, которые могут быть полностью выполнены в удаленной базе данных.</span><span class="sxs-lookup"><span data-stu-id="6531a-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="6531a-172">Для других шаблонов запросов может потребоваться загрузка больших объемов данных из удаленной базы данных, и эти шаблоны могут сработать неэффективно.</span><span class="sxs-lookup"><span data-stu-id="6531a-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6531a-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6531a-173">Next steps</span></span>

* <span data-ttu-id="6531a-174">Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6531a-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="6531a-175">Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="6531a-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="6531a-176">Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6531a-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="6531a-177">Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="6531a-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="6531a-178">В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.</span><span class="sxs-lookup"><span data-stu-id="6531a-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
