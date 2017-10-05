---
title: "Управление историческими данными в темпоральных таблицах с помощью политики хранения | Документация Microsoft"
description: "Узнайте, как использовать политику темпорального хранения для постоянного контроля над историческими данными."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: 8975d7a7d39114b2758d64a4df9f992cba6bf561
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="f4113-103">Управление историческими данными в темпоральных таблицах с политикой хранения</span><span class="sxs-lookup"><span data-stu-id="f4113-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="f4113-104">Темпоральные таблицы увеличивают размер базы данных больше, чем обычные таблицы, особенно если исторические данные хранятся в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="f4113-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="f4113-105">Поэтому политика хранения для исторических данных является важной составляющей управления жизненным циклом любой темпоральной таблицы.</span><span class="sxs-lookup"><span data-stu-id="f4113-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="f4113-106">Темпоральные таблицы в базе данных SQL Azure включают удобный механизм хранения, который помогает выполнить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="f4113-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="f4113-107">Темпоральное хранение исторических данных можно настроить на уровне отдельных таблиц. Это позволит пользователям использовать гибкие политики устаревания данных.</span><span class="sxs-lookup"><span data-stu-id="f4113-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span></span> <span data-ttu-id="f4113-108">Темпоральное хранение очень просто в применении: достаточно задать всего один параметр при создании таблицы или изменении схемы.</span><span class="sxs-lookup"><span data-stu-id="f4113-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span></span>

<span data-ttu-id="f4113-109">Когда вы определите политику хранения, база данных SQL Azure будет регулярно проверять, есть ли строки исторических данных, соответствующие условиям автоматической очистки.</span><span class="sxs-lookup"><span data-stu-id="f4113-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="f4113-110">Выявление и удаление строк в таблице исторических данных прозрачно выполняется в фоновой задаче, которая назначается и запускается самой системой.</span><span class="sxs-lookup"><span data-stu-id="f4113-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span></span> <span data-ttu-id="f4113-111">Условие устаревания для строк таблицы исторических данных проверяется по столбцу, представляющему окончание периода SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f4113-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="f4113-112">Например, если задан срок хранения 6 месяцев, подлежащие очистке строки таблицы будут удовлетворять следующему условию:</span><span class="sxs-lookup"><span data-stu-id="f4113-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="f4113-113">В приведенном выше примере мы предположили, что столбец **ValidTo** соответствует окончанию периода SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f4113-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span></span>

## <a name="how-to-configure-retention-policy"></a><span data-ttu-id="f4113-114">Настройка политики хранения</span><span class="sxs-lookup"><span data-stu-id="f4113-114">How to configure retention policy?</span></span>
<span data-ttu-id="f4113-115">Прежде чем настраивать политику хранения для темпоральной таблицы, проверьте, включена ли функция темпорального хранения исторических данных *на уровне базы данных*.</span><span class="sxs-lookup"><span data-stu-id="f4113-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="f4113-116">Флаг базы данных **is_temporal_history_retention_enabled** по умолчанию имеет значение ON (Вкл.), но пользователи могут изменить его с помощью инструкции ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="f4113-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="f4113-117">Он также автоматически получает значение OFF (Выкл.) после [восстановления до точки во времени](sql-database-recovery-using-backups.md).</span><span class="sxs-lookup"><span data-stu-id="f4113-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="f4113-118">Чтобы включить темпоральную очистку исторических данных для базы данных, выполните следующую инструкцию:</span><span class="sxs-lookup"><span data-stu-id="f4113-118">To enable temporal history retention cleanup for your database, execute the following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="f4113-119">Срок хранения для темпоральных таблиц можно настроить, даже если флаг **is_temporal_history_retention_enabled** имеет значение OFF, но в этом случае не будет активироваться автоматическая очистка для устаревших строк.</span><span class="sxs-lookup"><span data-stu-id="f4113-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="f4113-120">Политика хранения настраивается во время создания таблицы. Для этого нужно указать значение для параметра HISTORY_RETENTION_PERIOD:</span><span class="sxs-lookup"><span data-stu-id="f4113-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="f4113-121">База данных SQL Azure позволяет указать срок хранения, используя различные единицы времени: DAYS (дни), WEEKS (недели), MONTHS (месяцы) и YEARS (годы).</span><span class="sxs-lookup"><span data-stu-id="f4113-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="f4113-122">Если параметр HISTORY_RETENTION_PERIOD не указан, подразумевается неограниченное хранение (INFINITE).</span><span class="sxs-lookup"><span data-stu-id="f4113-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="f4113-123">Его также можно настроить, явно указав ключевое слово INFINITE.</span><span class="sxs-lookup"><span data-stu-id="f4113-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="f4113-124">Иногда требуется настроить политику хранения уже после создания таблицы или изменить настроенное ранее значение.</span><span class="sxs-lookup"><span data-stu-id="f4113-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span></span> <span data-ttu-id="f4113-125">В этом случае используйте инструкцию ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="f4113-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="f4113-126">Если для параметра SYSTEM_VERSIONING задать значение OFF, значение срока хранения *не сохраняется*.</span><span class="sxs-lookup"><span data-stu-id="f4113-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span></span> <span data-ttu-id="f4113-127">Если для параметра SYSTEM_VERSIONING задать значение ON, не указывая явно значение HISTORY_RETENTION_PERIOD, будет установлен неограниченный (INFINITE) срок хранения.</span><span class="sxs-lookup"><span data-stu-id="f4113-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="f4113-128">Чтобы просмотреть текущее состояние политики хранения, используйте следующий запрос, который объединяет флаг включения темпорального хранения на уровне базы данных со сроками хранения для отдельных таблиц:</span><span class="sxs-lookup"><span data-stu-id="f4113-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="f4113-129">Как база данных SQL удаляет устаревшие строки?</span><span class="sxs-lookup"><span data-stu-id="f4113-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="f4113-130">Процесс очистки зависит от структуры индексов таблицы исторических данных.</span><span class="sxs-lookup"><span data-stu-id="f4113-130">The cleanup process depends on the index layout of the history table.</span></span> <span data-ttu-id="f4113-131">Обратите внимание, что *политику хранения с ограниченным сроком можно настроить только для таблиц исторических данных с кластеризованным индексом (сбалансированное дерево или columnstore)*.</span><span class="sxs-lookup"><span data-stu-id="f4113-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="f4113-132">Для очистки устаревших данных из всех темпоральных таблиц с ограниченным сроком хранения создается фоновая задача.</span><span class="sxs-lookup"><span data-stu-id="f4113-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="f4113-133">Логика очистки для кластеризованного индекса типа rowstore (сбалансированное дерево) удаляет устаревшие строки мелкими фрагментами (не более 10 000), чтобы свести к минимуму нагрузку на журнал базы данных и подсистему ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="f4113-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="f4113-134">Несмотря на то что логика очистки использует индекс сбалансированного дерева, порядок удаления строк, возраст которых превышает срок хранения, не может быть гарантирован.</span><span class="sxs-lookup"><span data-stu-id="f4113-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="f4113-135">Поэтому *не используйте в приложениях никакие зависимости от порядка очистки*.</span><span class="sxs-lookup"><span data-stu-id="f4113-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span></span>

<span data-ttu-id="f4113-136">Задача очистки для кластеризованного индекса columnstore удаляет полные [группы строк](https://msdn.microsoft.com/library/gg492088.aspx) за один раз (обычно они содержат по миллиону строк). Это очень эффективный механизм, особенно если исторические данные формируются с высокой скоростью.</span><span class="sxs-lookup"><span data-stu-id="f4113-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Хранение кластеризованных индексов columnstore](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="f4113-138">Благодаря высокой эффективности сжатия данных и очистки кластеризованный индекс columnstore будет идеальным выбором для ситуаций, когда рабочая нагрузка быстро создает большие объемы исторических данных.</span><span class="sxs-lookup"><span data-stu-id="f4113-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="f4113-139">Этот шаблон традиционно используется для интенсивных [рабочих нагрузок с обработкой транзакций, использующих темпоральные таблицы](https://msdn.microsoft.com/library/mt631669.aspx), позволяя отслеживать изменения, проводить аудит и анализ тенденций, а также принимать данные от систем Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f4113-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="f4113-140">Рекомендации по выбору индекса</span><span class="sxs-lookup"><span data-stu-id="f4113-140">Index considerations</span></span>
<span data-ttu-id="f4113-141">Задача очистки для таблиц с кластеризованным индексом rowstore требует, чтобы индекс начинался со столбца, соответствующего окончанию периода SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f4113-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span></span> <span data-ttu-id="f4113-142">Если такого индекса не существует, вы не сможете настроить хранение с ограниченным сроком.</span><span class="sxs-lookup"><span data-stu-id="f4113-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="f4113-143">*Сообщение 13765, уровень 16, состояние 1 <br></br> Установка ограниченного срока хранения для темпоральной таблицы с системным управлением версиями temporalstagetestdb.dbo.WebsiteUserInfo завершилась сбоем, так как таблица исторических данных temporalstagetestdb.dbo.WebsiteUserInfoHistory не содержит требуемый кластеризованный индекс. Создайте в таблице исторических данных кластеризованный индекс columnstore или индекс сбалансированного дерева, начинающийся со столбца, который соответствует окончанию периода SYSTEM_TIME.*</span><span class="sxs-lookup"><span data-stu-id="f4113-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span></span>

<span data-ttu-id="f4113-144">Важно заметить, что таблица исторических данных по умолчанию, созданная базой данных SQL Azure, уже включает кластеризованный индекс, совместимый с политикой хранения.</span><span class="sxs-lookup"><span data-stu-id="f4113-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="f4113-145">При попытке удаления такого индекса для таблицы с ограниченным сроком хранения операция завершается следующей ошибкой:</span><span class="sxs-lookup"><span data-stu-id="f4113-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span></span>

<span data-ttu-id="f4113-146">*Сообщение 13766, уровень 16, состояние 1 <br></br> Не удается удалить кластеризованный индекс WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory, так как он используется для автоматической очистки устаревших данных. Если вам нужно удалить этот индекс, попробуйте задать для параметра HISTORY_RETENTION_PERIOD значение INFINITE для соответствующей темпоральной таблицы с системным управлением версиями.*</span><span class="sxs-lookup"><span data-stu-id="f4113-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span></span>

<span data-ttu-id="f4113-147">Очистка в кластеризованном индексе columnstore работает лучше всего, если строки исторических данных вставляются в порядке возрастания (с сортировкой по столбцу окончания периода). Это условие выполняется всегда, если таблицы исторических данных заполняются исключительно с помощью механизма SYSTEM_VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="f4113-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="f4113-148">Если строки в исторической таблице не упорядочены по столбцу окончания периода (это возможно, если выполнялась миграция существующих исторических данных), нужно заново создать кластеризованный индекс columnstore. Для оптимальной производительности создавайте его поверх правильно отсортированного индекса сбалансированного дерева rowstore.</span><span class="sxs-lookup"><span data-stu-id="f4113-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span></span>

<span data-ttu-id="f4113-149">Старайтесь не перестраивать кластеризованный индекс columnstore для таблицы исторических данных с ограниченным сроком хранения, так как это может изменить порядок групп строк, естественным образом созданный в результате работы системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="f4113-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span></span> <span data-ttu-id="f4113-150">Если необходимо перестроить кластеризованный индекс columnstore для таблицы исторических данных, создавайте его поверх правильного индекса сбалансированного дерева, чтобы сохранить в группах строк порядок, необходимый для регулярной очистки данных.</span><span class="sxs-lookup"><span data-stu-id="f4113-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="f4113-151">Аналогичный подход следует применять и при создании темпоральной таблицы из существующей таблицы исторических данных с кластеризованным индексом столбцов, но без гарантированного порядка данных:</span><span class="sxs-lookup"><span data-stu-id="f4113-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by the end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="f4113-152">Если вы настроите ограниченный срок хранения для таблицы исторических данных с кластеризованным индексом columnstore, вы не сможете создавать дополнительные некластеризованные индексы сбалансированного дерева для этой таблицы:</span><span class="sxs-lookup"><span data-stu-id="f4113-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="f4113-153">Попытка выполнить приведенную выше инструкцию завершится следующей ошибкой.</span><span class="sxs-lookup"><span data-stu-id="f4113-153">An attempt to execute above statement fails with the following error:</span></span>

<span data-ttu-id="f4113-154">*Сообщение 13772, уровень 16, состояние 1 <br></br> Не удалось создать некластеризованный индекс в темпоральной таблице исторических данных WebsiteUserInfoHistory, так как она имеет ограниченный срок хранения и для нее определен кластеризованный индекс columnstore.*</span><span class="sxs-lookup"><span data-stu-id="f4113-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="f4113-155">Запросы к таблицам с политикой хранения</span><span class="sxs-lookup"><span data-stu-id="f4113-155">Querying tables with retention policy</span></span>
<span data-ttu-id="f4113-156">Все запросы к темпоральным таблицам автоматически фильтруют строки исторических данных в соответствии с политикой ограниченного срока хранения. Это позволяет избежать непредсказуемости и несогласованности результатов, так как задача очистки может удалять устаревшие строки *в любой момент времени и в произвольном порядке*.</span><span class="sxs-lookup"><span data-stu-id="f4113-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="f4113-157">На следующем рисунке показан план для простого запроса.</span><span class="sxs-lookup"><span data-stu-id="f4113-157">The following picture shows the query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="f4113-158">План запроса содержит дополнительный фильтр, применяемый к столбцу окончания периода (ValidTo) в операторе "Clustered Index Scan" (Сканирование кластеризованного индекса) в таблице исторических данных (выделено).</span><span class="sxs-lookup"><span data-stu-id="f4113-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span></span> <span data-ttu-id="f4113-159">В этом примере предполагается, что для таблицы WebsiteUserInfo задан срок хранения "1 MONTH" (1 месяц).</span><span class="sxs-lookup"><span data-stu-id="f4113-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Фильтр для запроса хранения](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="f4113-161">Но если вы будете запрашивать таблицы исторических данных напрямую, результат может включать строки старше указанного периода хранения. При этом нет никаких гарантий, что повторные запросы вернут такие же результаты.</span><span class="sxs-lookup"><span data-stu-id="f4113-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="f4113-162">На следующем рисунке показан план выполнения для запроса в таблице исторических данных без применения дополнительных фильтров.</span><span class="sxs-lookup"><span data-stu-id="f4113-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span></span>

![Запрос по историческим данным без фильтра хранения](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="f4113-164">Не следует основывать бизнес-логику приложения на считывании таблицы исторических данных по окончании срока хранения. В таком случае вы можете получить несогласованные или непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="f4113-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="f4113-165">Мы рекомендуем использовать для анализа данных в темпоральных таблицах только темпоральные запросы с предложением FOR SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f4113-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="f4113-166">Рекомендации по восстановлению до точки во времени</span><span class="sxs-lookup"><span data-stu-id="f4113-166">Point in time restore considerations</span></span>
<span data-ttu-id="f4113-167">При создании новой базы данных путем [восстановления базы данных до определенной точки во времени](sql-database-recovery-using-backups.md) темпоральное хранение отключается на уровне базы данных.</span><span class="sxs-lookup"><span data-stu-id="f4113-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span></span> <span data-ttu-id="f4113-168">(Флаг **is_temporal_history_retention_enabled** получает значение OFF.)</span><span class="sxs-lookup"><span data-stu-id="f4113-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span></span> <span data-ttu-id="f4113-169">Эта функция позволяет изучить все строки исторических данных после восстановления, не беспокоясь, что устаревшие строки будут удалены еще до отправки запроса к ним.</span><span class="sxs-lookup"><span data-stu-id="f4113-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span></span> <span data-ttu-id="f4113-170">Используйте этот режим для *изучения исторических данных по окончании установленного срока хранения*.</span><span class="sxs-lookup"><span data-stu-id="f4113-170">You can use it to *inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="f4113-171">Предположим, что для темпоральной таблицы задан срок хранения в 1 месяц.</span><span class="sxs-lookup"><span data-stu-id="f4113-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="f4113-172">Если база данных создана на уровне службы "Премиум", вы сможете создать копию базы данных с состоянием базы данных за последние 35 дней.</span><span class="sxs-lookup"><span data-stu-id="f4113-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span></span> <span data-ttu-id="f4113-173">Это фактически позволит вам анализировать строки исторических данных за период до 65 дней с помощью прямых запросов к таблице исторических данных.</span><span class="sxs-lookup"><span data-stu-id="f4113-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span></span>

<span data-ttu-id="f4113-174">Если вы хотите активировать очистку темпорального хранения, выполните следующую инструкцию Transact-SQL после восстановления до точки во времени:</span><span class="sxs-lookup"><span data-stu-id="f4113-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="f4113-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4113-175">Next steps</span></span>
<span data-ttu-id="f4113-176">Чтобы узнать, как использовать темпоральные таблицы в приложениях, ознакомьтесь со статьей [Приступая к работе с временными таблицами в базе данных SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="f4113-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="f4113-177">Посетите сайт Channel 9, чтобы услышать [историю успешного внедрения темпоральных решений реальным клиентом](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) и просмотреть [наглядную демонстрацию темпоральных решений](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="f4113-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="f4113-178">Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4113-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

