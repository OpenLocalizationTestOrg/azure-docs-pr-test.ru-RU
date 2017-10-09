---
title: "aaaExtended события в базе данных SQL | Документы Microsoft"
description: "В статье описываются расширенные события (XEvents) в Базе данных SQL Azure и отличия соответствующих сеансов событий от сеансов событий в Microsoft SQL Server."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="62899-103">Расширенные события в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="62899-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="62899-104">Этот разделе объясняется, как реализация hello расширенных событий в базе данных SQL Azure немного отличается сравниваемых tooextended событий в Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="62899-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="62899-105">Базы данных SQL V12 приобретенные функции hello расширенных событий в hello второй половине календаря 2015.</span><span class="sxs-lookup"><span data-stu-id="62899-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="62899-106">SQL Server включает расширенные события с 2008 года.</span><span class="sxs-lookup"><span data-stu-id="62899-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="62899-107">набор функций Hello расширенных событий в базе данных SQL является надежным подмножество функций hello на сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="62899-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="62899-108">*XEvents* — это неофициальное обозначение расширенных событий, которое встречается в блоках и других неофициальных источниках.</span><span class="sxs-lookup"><span data-stu-id="62899-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="62899-109">Дополнительные сведения о расширенных событиях для базы данных SQL Azure и Microsoft SQL Server доступны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="62899-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="62899-110">Quick Start: Extended events in SQL Server</span><span class="sxs-lookup"><span data-stu-id="62899-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="62899-111">Расширенные события</span><span class="sxs-lookup"><span data-stu-id="62899-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="62899-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62899-112">Prerequisites</span></span>

<span data-ttu-id="62899-113">В данной статье предполагается, чтобы вы уже ознакомились со следующими компонентами:</span><span class="sxs-lookup"><span data-stu-id="62899-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="62899-114">[Служба Базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/);</span><span class="sxs-lookup"><span data-stu-id="62899-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="62899-115">[Расширенные события](http://msdn.microsoft.com/library/bb630282.aspx) в Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="62899-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="62899-116">Hello большая часть документации о расширенных событий применяется tooboth SQL Server и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="62899-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="62899-117">Предыдущий раскрытия toohello следующих элементов полезно при выборе файла событий как hello hello [целевой](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="62899-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="62899-118">Служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="62899-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="62899-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62899-119">PowerShell</span></span>
    - <span data-ttu-id="62899-120">[С помощью Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md) -предоставляет подробные сведения о службе хранилища Azure hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62899-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="62899-121">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="62899-121">Code samples</span></span>

<span data-ttu-id="62899-122">Связанные разделы содержат два примера кода.</span><span class="sxs-lookup"><span data-stu-id="62899-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="62899-123">Код целевого объекта "Кольцевой буфер" для расширенных событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="62899-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="62899-124">Простой короткий сценарий Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="62899-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="62899-125">Мы подчеркнуть hello кода образца раздела, что после завершения целевой кольцевой буфер должен освободить ресурсы, его, выполнив перетаскивания alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` инструкции.</span><span class="sxs-lookup"><span data-stu-id="62899-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="62899-126">Впоследствии вы сможете добавить другой экземпляр кольцевого буфера с помощью оператора `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="62899-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="62899-127">Код целевого объекта "Файл событий" для расширенных событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="62899-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="62899-128">Этап 1 — PowerShell toocreate контейнер службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="62899-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="62899-129">Этап 2 — Transact-SQL, использующего hello контейнер хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="62899-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="62899-130">Отличия Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="62899-130">Transact-SQL differences</span></span>


- <span data-ttu-id="62899-131">При выполнении hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) команды на сервере SQL Server использовать hello **ON SERVER** предложения.</span><span class="sxs-lookup"><span data-stu-id="62899-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="62899-132">Но в базе данных SQL используйте hello **ON DATABASE** предложение вместо него.</span><span class="sxs-lookup"><span data-stu-id="62899-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="62899-133">Hello **ON DATABASE** предложение также применяется toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) и [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) команд Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="62899-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="62899-134">Лучший способ — это параметр сеанса событий tooinclude hello объекта **STARTUP_STATE = ON** в ваш **CREATE EVENT SESSION** или **ALTER EVENT SESSION** инструкции.</span><span class="sxs-lookup"><span data-stu-id="62899-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="62899-135">Hello **= ON** значение поддерживает автоматический перезапуск после перенастройки hello логическую базу данных из-за tooa перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="62899-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="62899-136">Новые представления каталога</span><span class="sxs-lookup"><span data-stu-id="62899-136">New catalog views</span></span>

<span data-ttu-id="62899-137">Hello расширенных событий поддерживается несколько [представления каталога](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="62899-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="62899-138">Представления каталога сообщают об *метаданных и определений* сеансов событий, созданных пользователем в текущей базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="62899-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="62899-139">представления Hello не возвращают сведения об экземплярах сеансов активных событий.</span><span class="sxs-lookup"><span data-stu-id="62899-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="62899-140">Имя</span><span class="sxs-lookup"><span data-stu-id="62899-140">Name of</span></span><br/><span data-ttu-id="62899-141">представления каталога</span><span class="sxs-lookup"><span data-stu-id="62899-141">catalog view</span></span> | <span data-ttu-id="62899-142">Описание</span><span class="sxs-lookup"><span data-stu-id="62899-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="62899-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="62899-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="62899-144">Возвращает строку для каждого действия с каждым событием в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="62899-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="62899-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="62899-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="62899-146">Возвращает строку для каждого события в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="62899-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="62899-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="62899-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="62899-148">Возвращает строку для каждого настраиваемого столбца, который можно прямо задавать для событий и целевых объектов.</span><span class="sxs-lookup"><span data-stu-id="62899-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="62899-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="62899-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="62899-150">Возвращает строку для каждого целевого объекта события в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="62899-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="62899-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="62899-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="62899-152">Возвращает строку для каждого сеанса событий в базе данных hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="62899-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="62899-153">В Microsoft SQL Server аналогичные представления каталогов имеют имена, содержащие *.server\_* вместо *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="62899-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="62899-154">шаблон имени Hello аналогичен **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="62899-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="62899-155">Новые динамические административные представления [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="62899-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="62899-156">База данных SQL Azure включает [динамические административные представления (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) , которые поддерживают расширенные события.</span><span class="sxs-lookup"><span data-stu-id="62899-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="62899-157">DMV сообщают об *активных* сеансах событий.</span><span class="sxs-lookup"><span data-stu-id="62899-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="62899-158">Имя DMV</span><span class="sxs-lookup"><span data-stu-id="62899-158">Name of DMV</span></span> | <span data-ttu-id="62899-159">Описание</span><span class="sxs-lookup"><span data-stu-id="62899-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="62899-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="62899-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="62899-161">Возвращает сведения о действиях в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="62899-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="62899-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="62899-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="62899-163">Возвращает сведения о событиях в сеансе.</span><span class="sxs-lookup"><span data-stu-id="62899-163">Returns information about session events.</span></span> |
| <span data-ttu-id="62899-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="62899-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="62899-165">Отображает значения конфигурации hello объекты, которые являются tooa связанного сеанса.</span><span class="sxs-lookup"><span data-stu-id="62899-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="62899-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="62899-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="62899-167">Возвращает сведения о целевых объектах сеанса.</span><span class="sxs-lookup"><span data-stu-id="62899-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="62899-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="62899-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="62899-169">Возвращает по строке для каждого сеанса событий, является toohello области текущей базы данных.</span><span class="sxs-lookup"><span data-stu-id="62899-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="62899-170">В Microsoft SQL Server, аналогичные представления каталога с именем без hello  *\_базы данных* часть hello имя, такое как:</span><span class="sxs-lookup"><span data-stu-id="62899-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="62899-171">**sys.dm_xe_sessions** вместо имени</span><span class="sxs-lookup"><span data-stu-id="62899-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="62899-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="62899-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="62899-173">Общие tooboth динамических административных представлений</span><span class="sxs-lookup"><span data-stu-id="62899-173">DMVs common tooboth</span></span>
<span data-ttu-id="62899-174">Для расширенных событий существуют дополнительные динамические административные представления, общие tooboth базы данных SQL Azure и Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="62899-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="62899-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="62899-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="62899-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="62899-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="62899-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="62899-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="62899-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="62899-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="62899-179">Найти hello доступных расширенных событий, действия и целевые объекты</span><span class="sxs-lookup"><span data-stu-id="62899-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="62899-180">Можно выполнить простые SQL **ВЫБЕРИТЕ** tooobtain список доступных событий hello, действия и целевой объект.</span><span class="sxs-lookup"><span data-stu-id="62899-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="62899-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="62899-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="62899-182">Целевые объекты для сеансов событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="62899-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="62899-183">Результаты сеансов событий в Базе данных SQL можно фиксировать в следующих целевых объектах:</span><span class="sxs-lookup"><span data-stu-id="62899-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="62899-184">[Целевой объект "Кольцевой буфер"](http://msdn.microsoft.com/library/ff878182.aspx) — сохраняет данные события в памяти на недолгое время.</span><span class="sxs-lookup"><span data-stu-id="62899-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="62899-185">[Целевой объект "Счетчик событий"](http://msdn.microsoft.com/library/ff878025.aspx) — подсчитывает все события, произошедшие за время сеанса расширенных событий.</span><span class="sxs-lookup"><span data-stu-id="62899-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="62899-186">[Целевого файла событий](http://msdn.microsoft.com/library/ff878115.aspx) -контейнер хранилища Azure tooan запись всех буферов.</span><span class="sxs-lookup"><span data-stu-id="62899-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="62899-187">Hello [трассировки событий для Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API недоступен для расширенных событий в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="62899-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="62899-188">Ограничения</span><span class="sxs-lookup"><span data-stu-id="62899-188">Restrictions</span></span>

<span data-ttu-id="62899-189">Существует несколько различий, связанных с безопасностью befitting hello облачной среде базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="62899-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="62899-190">Расширенные события основанная на hello модель изоляции одного клиента.</span><span class="sxs-lookup"><span data-stu-id="62899-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="62899-191">Сеанс событий в одной базе данных не может получить доступ к данным или событиям в другой базе данных.</span><span class="sxs-lookup"><span data-stu-id="62899-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="62899-192">Не удается выпустить **CREATE EVENT SESSION** инструкции в контексте hello hello **master** базы данных.</span><span class="sxs-lookup"><span data-stu-id="62899-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="62899-193">Модель разрешений</span><span class="sxs-lookup"><span data-stu-id="62899-193">Permission model</span></span>

<span data-ttu-id="62899-194">Необходимо иметь **управления** разрешений на базу данных tooissue hello **CREATE EVENT SESSION** инструкции.</span><span class="sxs-lookup"><span data-stu-id="62899-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="62899-195">Hello владельца базы данных (dbo) имеет **управления** разрешение.</span><span class="sxs-lookup"><span data-stu-id="62899-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="62899-196">Авторизации контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="62899-196">Storage container authorizations</span></span>

<span data-ttu-id="62899-197">можно создавать для контейнера хранилища Azure необходимо указать имя маркера SAS Hello **rwl** для разрешения hello.</span><span class="sxs-lookup"><span data-stu-id="62899-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="62899-198">Hello **rwl** значение обеспечивает hello следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="62899-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="62899-199">чтение</span><span class="sxs-lookup"><span data-stu-id="62899-199">Read</span></span>
- <span data-ttu-id="62899-200">запись</span><span class="sxs-lookup"><span data-stu-id="62899-200">Write</span></span>
- <span data-ttu-id="62899-201">список</span><span class="sxs-lookup"><span data-stu-id="62899-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="62899-202">Рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="62899-202">Performance considerations</span></span>

<span data-ttu-id="62899-203">Существуют сценарии, где интенсивное использование расширенных событий могут накапливаться более активной памяти, не находится в работоспособном состоянии для hello системы в целом.</span><span class="sxs-lookup"><span data-stu-id="62899-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="62899-204">Таким образом hello системы базы данных SQL Azure динамически устанавливает и настраивает ограничения на объем hello активной памяти, которая суммируется сеанс событий.</span><span class="sxs-lookup"><span data-stu-id="62899-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="62899-205">Многие факторы углубляться динамическое вычисление hello.</span><span class="sxs-lookup"><span data-stu-id="62899-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="62899-206">При появлении сообщения о превышении максимального объема памяти можно предпринять следующие коррекционные меры:</span><span class="sxs-lookup"><span data-stu-id="62899-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="62899-207">уменьшить количество одновременно запущенных сеансов событий;</span><span class="sxs-lookup"><span data-stu-id="62899-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="62899-208">Через ваш **создать** и **ALTER** инструкции для сеансов событий уменьшения hello объема памяти, укажите на hello **MAX\_памяти** предложения.</span><span class="sxs-lookup"><span data-stu-id="62899-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="62899-209">Задержки сети</span><span class="sxs-lookup"><span data-stu-id="62899-209">Network latency</span></span>

<span data-ttu-id="62899-210">Hello **файла событий** целевой могут возникать задержки в сети или сбои во время сохранения tooAzure данных хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="62899-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="62899-211">Другие события в базе данных SQL может быть отложен ожидании toocomplete связи сети hello.</span><span class="sxs-lookup"><span data-stu-id="62899-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="62899-212">Такая задержка может замедлить вашу работу.</span><span class="sxs-lookup"><span data-stu-id="62899-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="62899-213">toomitigate производительности этот риск, не задавайте hello **EVENT_RETENTION_MODE** параметр слишком**NO_EVENT_LOSS** в определениях сеанса событий.</span><span class="sxs-lookup"><span data-stu-id="62899-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="62899-214">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="62899-214">Related links</span></span>

- <span data-ttu-id="62899-215">[Использование Azure PowerShell со службой хранилища Azure](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="62899-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="62899-216">Командлеты службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="62899-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="62899-217">[С помощью Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md) -предоставляет подробные сведения о службе хранилища Azure hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62899-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="62899-218">Как toouse хранилища BLOB-объектов из .NET</span><span class="sxs-lookup"><span data-stu-id="62899-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="62899-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="62899-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="62899-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="62899-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="62899-221">Публикации в блоге Джонтана Кехайаса (Jonathan Kehayias) о расширенных событий в Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="62899-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="62899-222">Hello Azure *обновления службы* веб-страницы, сужена tooAzure параметр базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="62899-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="62899-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="62899-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="62899-224">Другие разделы образец кода для расширенных событий доступны по ссылкам hello.</span><span class="sxs-lookup"><span data-stu-id="62899-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="62899-225">Тем не менее необходимо регулярно проверять любой образец toosee ли образец hello предназначен для Microsoft SQL Server и базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="62899-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="62899-226">Затем вы сможете решить, требуются ли незначительные изменения необходимые toorun образец hello.</span><span class="sxs-lookup"><span data-stu-id="62899-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
