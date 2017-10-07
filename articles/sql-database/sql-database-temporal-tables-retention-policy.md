---
title: "aaaManage данных журнала в Темпоральных таблицах с политикой хранения | Документы Microsoft"
description: "Узнайте, как toouse временного хранения tookeep исторические данные о политике под вашим управлением."
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
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="f16f7-103">Управление историческими данными в темпоральных таблицах с политикой хранения</span><span class="sxs-lookup"><span data-stu-id="f16f7-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="f16f7-104">Темпоральные таблицы увеличивают размер базы данных больше, чем обычные таблицы, особенно если исторические данные хранятся в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="f16f7-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="f16f7-105">Таким образом политика хранения исторических данных является важным аспектом планирования и управления жизненным циклом всех темпоральных таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="f16f7-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="f16f7-106">Темпоральные таблицы в базе данных SQL Azure включают удобный механизм хранения, который помогает выполнить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="f16f7-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="f16f7-107">Хранения журнала можно настроить на уровне hello отдельной таблицы, что позволяет пользователям гибкие срокам toocreate политик.</span><span class="sxs-lookup"><span data-stu-id="f16f7-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="f16f7-108">Применение временного хранения проста: требуется только один toobe параметр заданы во время создания или схемы изменением таблицы.</span><span class="sxs-lookup"><span data-stu-id="f16f7-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="f16f7-109">Когда вы определите политику хранения, база данных SQL Azure будет регулярно проверять, есть ли строки исторических данных, соответствующие условиям автоматической очистки.</span><span class="sxs-lookup"><span data-stu-id="f16f7-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="f16f7-110">Идентификация совпадающих строк и их удаление из таблицы журнала hello происходят прозрачно, в hello фоновой задачи, запланированные и запустите системой hello.</span><span class="sxs-lookup"><span data-stu-id="f16f7-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="f16f7-111">Возраст условия для строк таблицы журнала hello проверяется на основе столбца hello, представляющее конец периода SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f16f7-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="f16f7-112">Если срок хранения, например, имеет значение toosix месяцы, строк таблицы, подходящие для очистки удовлетворяют hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="f16f7-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="f16f7-113">В предыдущих пример hello, предполагается, что **ValidTo** столбец соответствует toohello окончания периода SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f16f7-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="f16f7-114">Как tooconfigure политики хранения?</span><span class="sxs-lookup"><span data-stu-id="f16f7-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="f16f7-115">Прежде чем настраивать политику хранения для темпоральной таблицы, сначала проверьте включен ли временного хранения исторических *на уровне базы данных hello*.</span><span class="sxs-lookup"><span data-stu-id="f16f7-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="f16f7-116">Базы данных флаг **is_temporal_history_retention_enabled** — tooON набор по умолчанию, но пользователи могут изменить с помощью инструкции ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="f16f7-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="f16f7-117">Кроме того, он автоматически tooOFF набор после [на момент времени восстановления](sql-database-recovery-using-backups.md) операции.</span><span class="sxs-lookup"><span data-stu-id="f16f7-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="f16f7-118">tooenable очистку хранения журнала для базы данных, выполните hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="f16f7-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="f16f7-119">Срок хранения для темпоральных таблиц можно настроить, даже если флаг **is_temporal_history_retention_enabled** имеет значение OFF, но в этом случае не будет активироваться автоматическая очистка для устаревших строк.</span><span class="sxs-lookup"><span data-stu-id="f16f7-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="f16f7-120">Настроена политика хранения во время создания таблицы путем указания значения для параметра HISTORY_RETENTION_PERIOD hello:</span><span class="sxs-lookup"><span data-stu-id="f16f7-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

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

<span data-ttu-id="f16f7-121">База данных SQL Azure позволяет toospecify срока хранения, используя различные единицы времени: дни, НЕДЕЛИ, МЕСЯЦЫ и ГОДЫ.</span><span class="sxs-lookup"><span data-stu-id="f16f7-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="f16f7-122">Если параметр HISTORY_RETENTION_PERIOD не указан, подразумевается неограниченное хранение (INFINITE).</span><span class="sxs-lookup"><span data-stu-id="f16f7-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="f16f7-123">Его также можно настроить, явно указав ключевое слово INFINITE.</span><span class="sxs-lookup"><span data-stu-id="f16f7-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="f16f7-124">В некоторых сценариях может потребоваться tooconfigure хранения после создания таблицы или toochange ранее настроенные значения.</span><span class="sxs-lookup"><span data-stu-id="f16f7-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="f16f7-125">В этом случае используйте инструкцию ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="f16f7-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="f16f7-126">Параметр SYSTEM_VERSIONING tooOFF *не сохраняет* срока хранения.</span><span class="sxs-lookup"><span data-stu-id="f16f7-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="f16f7-127">Параметр SYSTEM_VERSIONING tooON без HISTORY_RETENTION_PERIOD явным образом указано результаты в hello НЕОГРАНИЧЕННЫЙ срок хранения.</span><span class="sxs-lookup"><span data-stu-id="f16f7-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="f16f7-128">tooreview текущее состояние политики хранения hello, используйте hello следующий запрос флага включения хранения временных соединений на уровне базы данных hello со сроками хранения для отдельных таблиц:</span><span class="sxs-lookup"><span data-stu-id="f16f7-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

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


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="f16f7-129">Как база данных SQL удаляет устаревшие строки?</span><span class="sxs-lookup"><span data-stu-id="f16f7-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="f16f7-130">процесс очистки Hello зависит от макета индекс hello hello таблицы журнала.</span><span class="sxs-lookup"><span data-stu-id="f16f7-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="f16f7-131">Это важные toonotice, *таблицы журнала с кластеризованным индексом (B-дерева или columnstore) могут иметь конечное хранения политика, настроенная только*.</span><span class="sxs-lookup"><span data-stu-id="f16f7-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="f16f7-132">Фоновая задача создается tooperform очистки устаревших данных для всех временных таблиц с конечным срок.</span><span class="sxs-lookup"><span data-stu-id="f16f7-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="f16f7-133">Логика очистки для hello кластеризованный индекс rowstore (сбалансированное дерево) удаляет устаревшие строку небольшими фрагментами (вверх too10K), сводя к минимуму нагрузку на журнал базы данных и подсистемы ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="f16f7-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="f16f7-134">Несмотря на то, что используется логика очистки требуется индекс сбалансированного дерева, порядок удаления для hello строк, возраст которых превышает срок хранения не может быть гарантирована надежно.</span><span class="sxs-lookup"><span data-stu-id="f16f7-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="f16f7-135">Таким образом *не выполняют любую зависимость на порядок очистки hello в приложениях*.</span><span class="sxs-lookup"><span data-stu-id="f16f7-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="f16f7-136">Hello задача очистки для hello clustered columnstore удаляет всю [группы строк](https://msdn.microsoft.com/library/gg492088.aspx) за один раз (обычно содержит 1 миллион строк каждого), который очень эффективен, особенно в том случае, когда данные журнала создается с высокой скоростью.</span><span class="sxs-lookup"><span data-stu-id="f16f7-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Хранение кластеризованных индексов columnstore](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="f16f7-138">Благодаря высокой эффективности сжатия данных и очистки кластеризованный индекс columnstore будет идеальным выбором для ситуаций, когда рабочая нагрузка быстро создает большие объемы исторических данных.</span><span class="sxs-lookup"><span data-stu-id="f16f7-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="f16f7-139">Этот шаблон традиционно используется для интенсивных [рабочих нагрузок с обработкой транзакций, использующих темпоральные таблицы](https://msdn.microsoft.com/library/mt631669.aspx), позволяя отслеживать изменения, проводить аудит и анализ тенденций, а также принимать данные от систем Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f16f7-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="f16f7-140">Рекомендации по выбору индекса</span><span class="sxs-lookup"><span data-stu-id="f16f7-140">Index considerations</span></span>
<span data-ttu-id="f16f7-141">задача очистки Hello для таблиц с кластеризованный индекс rowstore требует toostart индекса с hello столбца соответствующий hello конец периода SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f16f7-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="f16f7-142">Если такого индекса не существует, вы не сможете настроить хранение с ограниченным сроком.</span><span class="sxs-lookup"><span data-stu-id="f16f7-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="f16f7-143">*Msg 13765, уровень 16, состояние 1 <br> </br> установки срока хранения конечное сбой временная таблица с системным управлением версиями «temporalstagetestdb.dbo.WebsiteUserInfo», поскольку hello таблицы журнала " temporalstagetestdb.dbo.WebsiteUserInfoHistory "не содержит обязательный кластеризованного индекса. Рекомендуется создать кластеризованный индекс columnstore или индекс сбалансированного дерева, начиная с hello столбец, который соответствует концу SYSTEM_TIME period в таблице журнала hello.*</span><span class="sxs-lookup"><span data-stu-id="f16f7-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="f16f7-144">Очень важно, что toonotice, hello таблица журнала по умолчанию, уже созданы в базе данных SQL Azure имеет кластеризованный индекс, который в соответствии с политикой хранения.</span><span class="sxs-lookup"><span data-stu-id="f16f7-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="f16f7-145">При попытке tooremove индекса для таблицы с конечным срок, происходит сбой операции с hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="f16f7-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="f16f7-146">*Msg 13766, уровень 16, состояние 1 <br> </br> невозможно удалить кластеризованный индекс hello «WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory», так как он используется для автоматического удаления устаревших данных. Рассмотрим параметр HISTORY_RETENTION_PERIOD tooINFINITE на соответствующий hello с системным управлением версиями временная таблица при необходимости toodrop этого индекса.*</span><span class="sxs-lookup"><span data-stu-id="f16f7-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="f16f7-147">Для очистки в кластеризованном индексе hello оптимальной работы при вставке строк журнала в возрастающем порядке (порядок концу hello столбец периода), всегда являющийся hello регистр при заполнении таблицы журнала hello монопольно hello SYSTEM_ hello Механизм VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="f16f7-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="f16f7-148">Если строки в таблице журнала hello не упорядочены по конец периода столбца (который может быть случай hello, при переносе существующего исторических данных), следует повторно создавать кластеризованный индекс на основе индекса rowstore сбалансированного дерева, надлежащим образом упорядочен, tooachieve оптимальной производительность.</span><span class="sxs-lookup"><span data-stu-id="f16f7-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="f16f7-149">Избегайте перестроение кластеризованного индекса columnstore в таблице журнала hello с периодом конечное хранения hello, поскольку он может измениться порядок групп строк Здравствуй естественным образом накладываемые hello операции системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="f16f7-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="f16f7-150">Если вам требуется toorebuild кластеризованный индекс columnstore в таблице журнала hello, для этого необходимо повторно создать его поверх совместимые индекс сбалансированного дерева, сохранение порядка в группах строк hello, необходимые для очистки обычных данных.</span><span class="sxs-lookup"><span data-stu-id="f16f7-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="f16f7-151">Привет, должна быть принята же подход, при создании временной таблицы с существующей таблицы журнала, имеет кластеризованный индекс столбца без порядок гарантированную данных:</span><span class="sxs-lookup"><span data-stu-id="f16f7-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="f16f7-152">При настройке срока хранения конечное для таблицы журнала hello с hello кластеризованный индекс нельзя создавать дополнительные некластеризованные индексы сбалансированного дерева для этой таблицы:</span><span class="sxs-lookup"><span data-stu-id="f16f7-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="f16f7-153">Попытка tooexecute выше инструкция завершается hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="f16f7-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="f16f7-154">*Сообщение 13772, уровень 16, состояние 1 <br></br> Не удалось создать некластеризованный индекс в темпоральной таблице исторических данных WebsiteUserInfoHistory, так как она имеет ограниченный срок хранения и для нее определен кластеризованный индекс columnstore.*</span><span class="sxs-lookup"><span data-stu-id="f16f7-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="f16f7-155">Запросы к таблицам с политикой хранения</span><span class="sxs-lookup"><span data-stu-id="f16f7-155">Querying tables with retention policy</span></span>
<span data-ttu-id="f16f7-156">Все запросы на hello временная таблица автоматически отфильтровать исторических строк конечное хранения политика сопоставления, tooavoid себя непредсказуемо и несогласованные результаты, так как устаревшие строки удаляются задачей очистки hello *в любой момент времени и в произвольный порядок*.</span><span class="sxs-lookup"><span data-stu-id="f16f7-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="f16f7-157">Hello следующем рисунке показан план запроса hello для простого запроса.</span><span class="sxs-lookup"><span data-stu-id="f16f7-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="f16f7-158">план включает дополнительный фильтр запросов Hello применять tooend периода столбца (ValidTo) в оператор Clustered Index Scan hello в таблице журнала hello (выделенной).</span><span class="sxs-lookup"><span data-stu-id="f16f7-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="f16f7-159">В этом примере предполагается, что для таблицы WebsiteUserInfo задан срок хранения "1 MONTH" (1 месяц).</span><span class="sxs-lookup"><span data-stu-id="f16f7-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Фильтр для запроса хранения](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="f16f7-161">Но если вы будете запрашивать таблицы исторических данных напрямую, результат может включать строки старше указанного периода хранения. При этом нет никаких гарантий, что повторные запросы вернут такие же результаты.</span><span class="sxs-lookup"><span data-stu-id="f16f7-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="f16f7-162">Hello следующем рисунке показан план выполнения запроса hello в таблице журнала hello без применения дополнительных фильтров.</span><span class="sxs-lookup"><span data-stu-id="f16f7-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Запрос по историческим данным без фильтра хранения](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="f16f7-164">Не следует основывать бизнес-логику приложения на считывании таблицы исторических данных по окончании срока хранения. В таком случае вы можете получить несогласованные или непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="f16f7-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="f16f7-165">Мы рекомендуем использовать для анализа данных в темпоральных таблицах только темпоральные запросы с предложением FOR SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="f16f7-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="f16f7-166">Рекомендации по восстановлению до точки во времени</span><span class="sxs-lookup"><span data-stu-id="f16f7-166">Point in time restore considerations</span></span>
<span data-ttu-id="f16f7-167">При создании новой базы данных по [восстановление существующей базы данных tooa определенный момент времени](sql-database-recovery-using-backups.md), он имеет временного хранения отключаются на уровне базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="f16f7-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="f16f7-168">(**is_temporal_history_retention_enabled** tooOFF установлен флаг).</span><span class="sxs-lookup"><span data-stu-id="f16f7-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="f16f7-169">Эта функция позволяет tooexamine удаляются все исторических строки, при восстановлении, не беспокоясь, устаревших строк, прежде чем получить tooquery их.</span><span class="sxs-lookup"><span data-stu-id="f16f7-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="f16f7-170">Можно использовать слишком*проверки исторических данных за пределы заданного срока хранения*.</span><span class="sxs-lookup"><span data-stu-id="f16f7-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="f16f7-171">Предположим, что для темпоральной таблицы задан срок хранения в 1 месяц.</span><span class="sxs-lookup"><span data-stu-id="f16f7-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="f16f7-172">Если база данных была создана на уровне служб Premium, то может оказаться копия базы данных может toocreate с состоянием базы данных hello вверх too35 дней в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="f16f7-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="f16f7-173">Которое фактически позволило бы вы tooanalyze исторических строк, которые функционируют too65 дней путем прямого запроса таблицы журнала hello.</span><span class="sxs-lookup"><span data-stu-id="f16f7-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="f16f7-174">Очистка временного хранения tooactivate запустите hello, следующем за инструкцией Transact-SQL после восстановления момент времени:</span><span class="sxs-lookup"><span data-stu-id="f16f7-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="f16f7-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f16f7-175">Next steps</span></span>
<span data-ttu-id="f16f7-176">как извлечь toouse временных таблиц в приложениях, toolearn [Приступая к работе с Темпоральными таблицами в базе данных SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="f16f7-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="f16f7-177">Посещение Channel 9 toohear [историю успеха temporal реализации реальных клиентских](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) » и «Контрольное [live temporal демонстрации](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="f16f7-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="f16f7-178">Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="f16f7-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

