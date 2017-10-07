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
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Управление историческими данными в темпоральных таблицах с политикой хранения
Темпоральные таблицы увеличивают размер базы данных больше, чем обычные таблицы, особенно если исторические данные хранятся в течение длительного времени. Таким образом политика хранения исторических данных является важным аспектом планирования и управления жизненным циклом всех темпоральных таблиц hello. Темпоральные таблицы в базе данных SQL Azure включают удобный механизм хранения, который помогает выполнить эту задачу.

Хранения журнала можно настроить на уровне hello отдельной таблицы, что позволяет пользователям гибкие срокам toocreate политик. Применение временного хранения проста: требуется только один toobe параметр заданы во время создания или схемы изменением таблицы.

Когда вы определите политику хранения, база данных SQL Azure будет регулярно проверять, есть ли строки исторических данных, соответствующие условиям автоматической очистки. Идентификация совпадающих строк и их удаление из таблицы журнала hello происходят прозрачно, в hello фоновой задачи, запланированные и запустите системой hello. Возраст условия для строк таблицы журнала hello проверяется на основе столбца hello, представляющее конец периода SYSTEM_TIME. Если срок хранения, например, имеет значение toosix месяцы, строк таблицы, подходящие для очистки удовлетворяют hello следующие условия:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

В предыдущих пример hello, предполагается, что **ValidTo** столбец соответствует toohello окончания периода SYSTEM_TIME.

## <a name="how-tooconfigure-retention-policy"></a>Как tooconfigure политики хранения?
Прежде чем настраивать политику хранения для темпоральной таблицы, сначала проверьте включен ли временного хранения исторических *на уровне базы данных hello*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Базы данных флаг **is_temporal_history_retention_enabled** — tooON набор по умолчанию, но пользователи могут изменить с помощью инструкции ALTER DATABASE. Кроме того, он автоматически tooOFF набор после [на момент времени восстановления](sql-database-recovery-using-backups.md) операции. tooenable очистку хранения журнала для базы данных, выполните hello следующей инструкцией:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> Срок хранения для темпоральных таблиц можно настроить, даже если флаг **is_temporal_history_retention_enabled** имеет значение OFF, но в этом случае не будет активироваться автоматическая очистка для устаревших строк.
> 
> 

Настроена политика хранения во время создания таблицы путем указания значения для параметра HISTORY_RETENTION_PERIOD hello:

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

База данных SQL Azure позволяет toospecify срока хранения, используя различные единицы времени: дни, НЕДЕЛИ, МЕСЯЦЫ и ГОДЫ. Если параметр HISTORY_RETENTION_PERIOD не указан, подразумевается неограниченное хранение (INFINITE). Его также можно настроить, явно указав ключевое слово INFINITE.

В некоторых сценариях может потребоваться tooconfigure хранения после создания таблицы или toochange ранее настроенные значения. В этом случае используйте инструкцию ALTER TABLE:

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Параметр SYSTEM_VERSIONING tooOFF *не сохраняет* срока хранения. Параметр SYSTEM_VERSIONING tooON без HISTORY_RETENTION_PERIOD явным образом указано результаты в hello НЕОГРАНИЧЕННЫЙ срок хранения.
> 
> 

tooreview текущее состояние политики хранения hello, используйте hello следующий запрос флага включения хранения временных соединений на уровне базы данных hello со сроками хранения для отдельных таблиц:

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


## <a name="how-sql-database-deletes-aged-rows"></a>Как база данных SQL удаляет устаревшие строки?
процесс очистки Hello зависит от макета индекс hello hello таблицы журнала. Это важные toonotice, *таблицы журнала с кластеризованным индексом (B-дерева или columnstore) могут иметь конечное хранения политика, настроенная только*. Фоновая задача создается tooperform очистки устаревших данных для всех временных таблиц с конечным срок.
Логика очистки для hello кластеризованный индекс rowstore (сбалансированное дерево) удаляет устаревшие строку небольшими фрагментами (вверх too10K), сводя к минимуму нагрузку на журнал базы данных и подсистемы ввода-вывода. Несмотря на то, что используется логика очистки требуется индекс сбалансированного дерева, порядок удаления для hello строк, возраст которых превышает срок хранения не может быть гарантирована надежно. Таким образом *не выполняют любую зависимость на порядок очистки hello в приложениях*.

Hello задача очистки для hello clustered columnstore удаляет всю [группы строк](https://msdn.microsoft.com/library/gg492088.aspx) за один раз (обычно содержит 1 миллион строк каждого), который очень эффективен, особенно в том случае, когда данные журнала создается с высокой скоростью.

![Хранение кластеризованных индексов columnstore](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

Благодаря высокой эффективности сжатия данных и очистки кластеризованный индекс columnstore будет идеальным выбором для ситуаций, когда рабочая нагрузка быстро создает большие объемы исторических данных. Этот шаблон традиционно используется для интенсивных [рабочих нагрузок с обработкой транзакций, использующих темпоральные таблицы](https://msdn.microsoft.com/library/mt631669.aspx), позволяя отслеживать изменения, проводить аудит и анализ тенденций, а также принимать данные от систем Интернета вещей.

## <a name="index-considerations"></a>Рекомендации по выбору индекса
задача очистки Hello для таблиц с кластеризованный индекс rowstore требует toostart индекса с hello столбца соответствующий hello конец периода SYSTEM_TIME. Если такого индекса не существует, вы не сможете настроить хранение с ограниченным сроком.

*Msg 13765, уровень 16, состояние 1 <br> </br> установки срока хранения конечное сбой временная таблица с системным управлением версиями «temporalstagetestdb.dbo.WebsiteUserInfo», поскольку hello таблицы журнала " temporalstagetestdb.dbo.WebsiteUserInfoHistory "не содержит обязательный кластеризованного индекса. Рекомендуется создать кластеризованный индекс columnstore или индекс сбалансированного дерева, начиная с hello столбец, который соответствует концу SYSTEM_TIME period в таблице журнала hello.*

Очень важно, что toonotice, hello таблица журнала по умолчанию, уже созданы в базе данных SQL Azure имеет кластеризованный индекс, который в соответствии с политикой хранения. При попытке tooremove индекса для таблицы с конечным срок, происходит сбой операции с hello следующая ошибка:

*Msg 13766, уровень 16, состояние 1 <br> </br> невозможно удалить кластеризованный индекс hello «WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory», так как он используется для автоматического удаления устаревших данных. Рассмотрим параметр HISTORY_RETENTION_PERIOD tooINFINITE на соответствующий hello с системным управлением версиями временная таблица при необходимости toodrop этого индекса.*

Для очистки в кластеризованном индексе hello оптимальной работы при вставке строк журнала в возрастающем порядке (порядок концу hello столбец периода), всегда являющийся hello регистр при заполнении таблицы журнала hello монопольно hello SYSTEM_ hello Механизм VERSIONIOING. Если строки в таблице журнала hello не упорядочены по конец периода столбца (который может быть случай hello, при переносе существующего исторических данных), следует повторно создавать кластеризованный индекс на основе индекса rowstore сбалансированного дерева, надлежащим образом упорядочен, tooachieve оптимальной производительность.

Избегайте перестроение кластеризованного индекса columnstore в таблице журнала hello с периодом конечное хранения hello, поскольку он может измениться порядок групп строк Здравствуй естественным образом накладываемые hello операции системы управления версиями. Если вам требуется toorebuild кластеризованный индекс columnstore в таблице журнала hello, для этого необходимо повторно создать его поверх совместимые индекс сбалансированного дерева, сохранение порядка в группах строк hello, необходимые для очистки обычных данных. Привет, должна быть принята же подход, при создании временной таблицы с существующей таблицы журнала, имеет кластеризованный индекс столбца без порядок гарантированную данных:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

При настройке срока хранения конечное для таблицы журнала hello с hello кластеризованный индекс нельзя создавать дополнительные некластеризованные индексы сбалансированного дерева для этой таблицы:

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Попытка tooexecute выше инструкция завершается hello следующая ошибка:

*Сообщение 13772, уровень 16, состояние 1 <br></br> Не удалось создать некластеризованный индекс в темпоральной таблице исторических данных WebsiteUserInfoHistory, так как она имеет ограниченный срок хранения и для нее определен кластеризованный индекс columnstore.*

## <a name="querying-tables-with-retention-policy"></a>Запросы к таблицам с политикой хранения
Все запросы на hello временная таблица автоматически отфильтровать исторических строк конечное хранения политика сопоставления, tooavoid себя непредсказуемо и несогласованные результаты, так как устаревшие строки удаляются задачей очистки hello *в любой момент времени и в произвольный порядок*.

Hello следующем рисунке показан план запроса hello для простого запроса.

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

план включает дополнительный фильтр запросов Hello применять tooend периода столбца (ValidTo) в оператор Clustered Index Scan hello в таблице журнала hello (выделенной). В этом примере предполагается, что для таблицы WebsiteUserInfo задан срок хранения "1 MONTH" (1 месяц).

![Фильтр для запроса хранения](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Но если вы будете запрашивать таблицы исторических данных напрямую, результат может включать строки старше указанного периода хранения. При этом нет никаких гарантий, что повторные запросы вернут такие же результаты. Hello следующем рисунке показан план выполнения запроса hello в таблице журнала hello без применения дополнительных фильтров.

![Запрос по историческим данным без фильтра хранения](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

Не следует основывать бизнес-логику приложения на считывании таблицы исторических данных по окончании срока хранения. В таком случае вы можете получить несогласованные или непредвиденные результаты. Мы рекомендуем использовать для анализа данных в темпоральных таблицах только темпоральные запросы с предложением FOR SYSTEM_TIME.

## <a name="point-in-time-restore-considerations"></a>Рекомендации по восстановлению до точки во времени
При создании новой базы данных по [восстановление существующей базы данных tooa определенный момент времени](sql-database-recovery-using-backups.md), он имеет временного хранения отключаются на уровне базы данных hello. (**is_temporal_history_retention_enabled** tooOFF установлен флаг). Эта функция позволяет tooexamine удаляются все исторических строки, при восстановлении, не беспокоясь, устаревших строк, прежде чем получить tooquery их. Можно использовать слишком*проверки исторических данных за пределы заданного срока хранения*.

Предположим, что для темпоральной таблицы задан срок хранения в 1 месяц. Если база данных была создана на уровне служб Premium, то может оказаться копия базы данных может toocreate с состоянием базы данных hello вверх too35 дней в прошлом hello. Которое фактически позволило бы вы tooanalyze исторических строк, которые функционируют too65 дней путем прямого запроса таблицы журнала hello.

Очистка временного хранения tooactivate запустите hello, следующем за инструкцией Transact-SQL после восстановления момент времени:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Дальнейшие действия
как извлечь toouse временных таблиц в приложениях, toolearn [Приступая к работе с Темпоральными таблицами в базе данных SQL Azure](sql-database-temporal-tables.md).

Посещение Channel 9 toohear [историю успеха temporal реализации реальных клиентских](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) » и «Контрольное [live temporal демонстрации](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Дополнительные сведения о темпоральных таблицах см. в [документации MSDN](https://msdn.microsoft.com/library/dn935015.aspx).

