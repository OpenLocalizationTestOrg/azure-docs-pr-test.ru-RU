---
title: "aaaReport масштабируемых облачных базах данных (горизонтальное секционирование) | Документы Microsoft"
description: "как toouse кросс-запросов к базе данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="b9b24-103">Отчеты по масштабируемым облачным базам данных (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="b9b24-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="b9b24-104">С помощью [эластичных запросов](sql-database-elastic-query-overview.md)можно создавать отчеты из нескольких баз данных SQL Azure из одной точки подключения.</span><span class="sxs-lookup"><span data-stu-id="b9b24-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="b9b24-105">Hello баз данных должны быть горизонтально секционированы (также называемая «сегментированных»).</span><span class="sxs-lookup"><span data-stu-id="b9b24-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="b9b24-106">При наличии существующей базы данных, в разделе [перенос существующих баз данных базы данных вне tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="b9b24-107">объекты SQL hello toounderstand нужны tooquery см. в разделе [запросов в нескольких базах данных горизонтально секционированные](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9b24-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9b24-108">Prerequisites</span></span>
<span data-ttu-id="b9b24-109">Загрузите и запустите hello [Приступая к работе с образцом эластичной базы данных средства](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="b9b24-110">Создать пример приложения hello с помощью диспетчера карты сегментов</span><span class="sxs-lookup"><span data-stu-id="b9b24-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="b9b24-111">Здесь вы создадите карта сегментов manager вместе с несколькими сегментами, следуют вставки данных в сегментах hello.</span><span class="sxs-lookup"><span data-stu-id="b9b24-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="b9b24-112">Если вы столкнулись tooalready установки сегментов с сегментированных данных в них, можно пропустить следующие шаги hello и переместить следующий раздел toohello.</span><span class="sxs-lookup"><span data-stu-id="b9b24-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="b9b24-113">Построение и запуск hello **Приступая к работе со средствами эластичной базы данных** образец приложения.</span><span class="sxs-lookup"><span data-stu-id="b9b24-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="b9b24-114">Выполните действия hello до шага 7 в разделе "hello" [загрузить и запустить пример приложения hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="b9b24-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="b9b24-115">В конце hello шаг 7 вы увидите hello, выполнив в командной строке:</span><span class="sxs-lookup"><span data-stu-id="b9b24-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![окно командной строки.][1]
2. <span data-ttu-id="b9b24-117">В окне приветствия командной строки, введите «1» и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="b9b24-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="b9b24-118">Это создает диспетчера карты сегментов hello и добавляет два сервера toohello сегментов.</span><span class="sxs-lookup"><span data-stu-id="b9b24-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="b9b24-119">Затем введите «3» и нажмите клавишу **ввод**; повторите действие hello четыре раза.</span><span class="sxs-lookup"><span data-stu-id="b9b24-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="b9b24-120">Это позволит вставить строки демонстрационных данных в свои сегменты.</span><span class="sxs-lookup"><span data-stu-id="b9b24-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="b9b24-121">Hello [портал Azure](https://portal.azure.com) должны отобразиться три новых баз данных сервера:</span><span class="sxs-lookup"><span data-stu-id="b9b24-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Подтверждение Visual Studio][2]

   <span data-ttu-id="b9b24-123">На этом этапе межбазовые запросы поддерживаются с помощью клиентских библиотек hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="b9b24-124">Например используйте параметр 4 в командном окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="b9b24-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="b9b24-125">Hello результаты из нескольких сегментов запроса всегда являются **UNION ALL** hello результатов из всех сегментах.</span><span class="sxs-lookup"><span data-stu-id="b9b24-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="b9b24-126">В следующем разделе hello мы создадим конечной точке образец базы данных, который поддерживает обширные возможности запрос hello данных по сегментам.</span><span class="sxs-lookup"><span data-stu-id="b9b24-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="b9b24-127">Создание запросов к эластичной базе данных</span><span class="sxs-lookup"><span data-stu-id="b9b24-127">Create an elastic query database</span></span>
1. <span data-ttu-id="b9b24-128">Откройте hello [портал Azure](https://portal.azure.com) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="b9b24-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="b9b24-129">Создать новую базу данных Azure SQL в hello же сервере, что настройки сегментов.</span><span class="sxs-lookup"><span data-stu-id="b9b24-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="b9b24-130">Имя базы данных hello «ElasticDBQuery».</span><span class="sxs-lookup"><span data-stu-id="b9b24-130">Name hello database "ElasticDBQuery."</span></span>

    ![Портал Azure и ценовая категория][3]

    > [!NOTE]
    > <span data-ttu-id="b9b24-132">Можно использовать существующую базу данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-132">you can use an existing database.</span></span> <span data-ttu-id="b9b24-133">Если это можно сделать, он не должен быть один из сегментов hello, желательно tooexecute ваших запросов.</span><span class="sxs-lookup"><span data-stu-id="b9b24-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="b9b24-134">Эта база данных будет использоваться для создания hello объекты метаданных для запроса эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="b9b24-135">Создание объектов базы данных</span><span class="sxs-lookup"><span data-stu-id="b9b24-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="b9b24-136">Главный ключ и учетные данные для конкретной базы данных</span><span class="sxs-lookup"><span data-stu-id="b9b24-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="b9b24-137">Это диспетчера карты сегментов toohello используется tooconnect и hello сегментов:</span><span class="sxs-lookup"><span data-stu-id="b9b24-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="b9b24-138">Откройте SQL Server Management Studio или SQL Server Data Tools в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9b24-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="b9b24-139">Подключите tooElasticDBQuery базы данных, выполните следующие команды T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="b9b24-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="b9b24-140">«username» и «password» должен быть hello же, как учетные данные, используемые в шаге 6 процедуры [загрузить и запустить пример приложения hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) в [Приступая к работе со средствами эластичной базы данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="b9b24-141">Внешние источники данных</span><span class="sxs-lookup"><span data-stu-id="b9b24-141">External data sources</span></span>
<span data-ttu-id="b9b24-142">toocreate внешнего источника данных, выполните следующую команду в базе данных ElasticDBQuery hello hello:</span><span class="sxs-lookup"><span data-stu-id="b9b24-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="b9b24-143">«CustomerIDShardMap» — hello имя карты сегментов hello, при создании карты сегментов hello и карты сегментов диспетчера с помощью средства образец hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="b9b24-144">Тем не менее если вы использовали пользовательские настройки для данного образца, затем следует имя сопоставления сегментов hello, выбранное в приложении.</span><span class="sxs-lookup"><span data-stu-id="b9b24-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="b9b24-145">Внешние таблицы</span><span class="sxs-lookup"><span data-stu-id="b9b24-145">External tables</span></span>
<span data-ttu-id="b9b24-146">Создайте внешнюю таблицу, которая соответствует таблицу Customers hello на сегменты hello, выполнив следующую команду в базе данных ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="b9b24-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="b9b24-147">Выполнение запроса T-SQL к примеру эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="b9b24-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="b9b24-148">После определения источника внешних данных и внешних таблиц теперь можно использовать полный T-SQL для внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="b9b24-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="b9b24-149">Выполните следующий запрос в базе данных ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="b9b24-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="b9b24-150">Можно заметить этого запроса hello объединяет результаты из всех сегментов hello и предоставляет hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b9b24-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Сведения о выходных данных][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="b9b24-152">Импорт tooExcel результаты запроса эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="b9b24-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="b9b24-153">Можно импортировать результаты hello из файла Excel tooan запроса.</span><span class="sxs-lookup"><span data-stu-id="b9b24-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="b9b24-154">Запустите Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="b9b24-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="b9b24-155">Перейдите toohello **данные** ленты.</span><span class="sxs-lookup"><span data-stu-id="b9b24-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="b9b24-156">Щелкните **Из других источников**, а затем — **Из SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b9b24-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Импорт в Excel из других источников][5]
4. <span data-ttu-id="b9b24-158">В hello **мастер подключения данных** введите учетные данные имя и имя входа сервера hello.</span><span class="sxs-lookup"><span data-stu-id="b9b24-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="b9b24-159">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9b24-159">Then click **Next**.</span></span>
5. <span data-ttu-id="b9b24-160">В диалоговом окне приветствия **hello выберите базу данных, содержащую данные hello**выберите hello **ElasticDBQuery** базы данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="b9b24-161">Выберите hello **клиентов** из таблицы в представлении списка hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9b24-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="b9b24-162">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b9b24-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="b9b24-163">В hello **импорта данных** форме, в разделе **выберите способ tooview эти данные в книге**выберите **таблицы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b9b24-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="b9b24-164">Здравствуйте, все строки из **клиентов** листа Excel hello заполнение таблицы, хранимые в разных сегментах.</span><span class="sxs-lookup"><span data-stu-id="b9b24-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="b9b24-165">Теперь можно использовать мощные функции Excel по визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="b9b24-166">Можно использовать строку подключения hello именем сервера, имя базы данных и учетные данные tooconnect бизнес-Аналитики и данные интеграции средства toohello запроса эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b9b24-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="b9b24-167">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b9b24-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="b9b24-168">Можно ссылаться toohello эластичной запрос к базе данных и внешних таблиц так же, как и любой другой базы данных SQL Server и таблицах SQL Server, то для подключения toowith средством.</span><span class="sxs-lookup"><span data-stu-id="b9b24-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="b9b24-169">Стоимость</span><span class="sxs-lookup"><span data-stu-id="b9b24-169">Cost</span></span>
<span data-ttu-id="b9b24-170">Без дополнительной платы применения функции hello запроса эластичной базы данных не существует.</span><span class="sxs-lookup"><span data-stu-id="b9b24-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="b9b24-171">Сведения о ценах см. на [странице с ценами на базу данных SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="b9b24-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9b24-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9b24-172">Next steps</span></span>

* <span data-ttu-id="b9b24-173">Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="b9b24-174">Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="b9b24-175">Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="b9b24-176">Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="b9b24-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="b9b24-177">В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.</span><span class="sxs-lookup"><span data-stu-id="b9b24-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
