---
title: "Расширенные события в базе данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="dfd4d-103">Расширенные события в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="dfd4d-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="dfd4d-104">В этом разделе объясняется, чем расширенные события в Базе данных SQL Azure отличается от расширенных событий в Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="dfd4d-105">В Базе данных SQL версии 12 функция расширенных событий появилась во второй половине 2015 года.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="dfd4d-106">SQL Server включает расширенные события с 2008 года.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="dfd4d-107">Набор функций расширенных событий в Базе данных SQL представляет собой устойчивое подмножество функций SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="dfd4d-108">*XEvents* — это неофициальное обозначение расширенных событий, которое встречается в блоках и других неофициальных источниках.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="dfd4d-109">Дополнительные сведения о расширенных событиях для базы данных SQL Azure и Microsoft SQL Server доступны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="dfd4d-110">Quick Start: Extended events in SQL Server</span><span class="sxs-lookup"><span data-stu-id="dfd4d-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="dfd4d-111">Расширенные события</span><span class="sxs-lookup"><span data-stu-id="dfd4d-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="dfd4d-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dfd4d-112">Prerequisites</span></span>

<span data-ttu-id="dfd4d-113">В данной статье предполагается, чтобы вы уже ознакомились со следующими компонентами:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="dfd4d-114">[Служба Базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/);</span><span class="sxs-lookup"><span data-stu-id="dfd4d-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="dfd4d-115">[Расширенные события](http://msdn.microsoft.com/library/bb630282.aspx) в Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="dfd4d-116">Большинство документации о расширенных событиях относится и к SQL Server, и к Базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="dfd4d-117">При выборе файла событий в качестве [целевого объекта](#AzureXEventsTargets)пригодится знание следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="dfd4d-118">Служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="dfd4d-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="dfd4d-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfd4d-119">PowerShell</span></span>
    - <span data-ttu-id="dfd4d-120">[Использование Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md) — статья содержит полную информацию о PowerShell и службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="dfd4d-121">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="dfd4d-121">Code samples</span></span>

<span data-ttu-id="dfd4d-122">Связанные разделы содержат два примера кода.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="dfd4d-123">Код целевого объекта "Кольцевой буфер" для расширенных событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="dfd4d-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="dfd4d-124">Простой короткий сценарий Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="dfd4d-125">В этой статье с примером кода подчеркивается, что после завершения работы с целевым объектом "Кольцевой буфер" необходимо освободить задействованные им ресурсы с помощью инструкции изменения и удаления `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` .</span><span class="sxs-lookup"><span data-stu-id="dfd4d-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="dfd4d-126">Впоследствии вы сможете добавить другой экземпляр кольцевого буфера с помощью оператора `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="dfd4d-127">Код целевого объекта "Файл событий" для расширенных событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="dfd4d-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="dfd4d-128">Этап 1. PowerShell: создание контейнера хранилища Azure в облаке.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="dfd4d-129">Этап 2. Transact-SQL: использование контейнера хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="dfd4d-130">Отличия Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="dfd4d-130">Transact-SQL differences</span></span>


- <span data-ttu-id="dfd4d-131">При выполнении команды [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) на сервере SQL Server используется предложение **ON SERVER** .</span><span class="sxs-lookup"><span data-stu-id="dfd4d-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="dfd4d-132">В Базе данных SQL вместо него используется предложение **ON DATABASE** .</span><span class="sxs-lookup"><span data-stu-id="dfd4d-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="dfd4d-133">Предложение **ON DATABASE** применяется также в командах Transact-SQL [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) и [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfd4d-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="dfd4d-134">Мы рекомендуем включать параметр сеанса событий **STARTUP_STATE = ON** в операторы **CREATE EVENT SESSION** и **ALTER EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="dfd4d-135">Значение **= ON** поддерживает автоматический перезапуск после перенастройки логической базы данных из-за сбоя.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="dfd4d-136">Новые представления каталога</span><span class="sxs-lookup"><span data-stu-id="dfd4d-136">New catalog views</span></span>

<span data-ttu-id="dfd4d-137">Функцию расширенных событий поддерживают несколько [представлений каталога](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfd4d-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="dfd4d-138">Представления каталога сообщают *метаданные или определения* сеансов событий, созданных пользователями в текущей базе данных.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="dfd4d-139">Представления не возвращают сведения об экземплярах активных сеансов событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="dfd4d-140">Имя</span><span class="sxs-lookup"><span data-stu-id="dfd4d-140">Name of</span></span><br/><span data-ttu-id="dfd4d-141">представления каталога</span><span class="sxs-lookup"><span data-stu-id="dfd4d-141">catalog view</span></span> | <span data-ttu-id="dfd4d-142">Описание</span><span class="sxs-lookup"><span data-stu-id="dfd4d-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dfd4d-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="dfd4d-144">Возвращает строку для каждого действия с каждым событием в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="dfd4d-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="dfd4d-146">Возвращает строку для каждого события в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="dfd4d-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="dfd4d-148">Возвращает строку для каждого настраиваемого столбца, который можно прямо задавать для событий и целевых объектов.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="dfd4d-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="dfd4d-150">Возвращает строку для каждого целевого объекта события в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="dfd4d-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="dfd4d-152">Возвращает строку для каждого сеанса событий в Базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="dfd4d-153">В Microsoft SQL Server аналогичные представления каталогов имеют имена, содержащие *.server\_* вместо *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="dfd4d-154">Шаблон имени выглядит как **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="dfd4d-155">Новые динамические административные представления [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="dfd4d-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="dfd4d-156">База данных SQL Azure включает [динамические административные представления (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) , которые поддерживают расширенные события.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="dfd4d-157">DMV сообщают об *активных* сеансах событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="dfd4d-158">Имя DMV</span><span class="sxs-lookup"><span data-stu-id="dfd4d-158">Name of DMV</span></span> | <span data-ttu-id="dfd4d-159">Описание</span><span class="sxs-lookup"><span data-stu-id="dfd4d-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dfd4d-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="dfd4d-161">Возвращает сведения о действиях в сеансе событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="dfd4d-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="dfd4d-163">Возвращает сведения о событиях в сеансе.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-163">Returns information about session events.</span></span> |
| <span data-ttu-id="dfd4d-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="dfd4d-165">Отображает значения конфигурации для объектов, привязанных к сеансу.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="dfd4d-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="dfd4d-167">Возвращает сведения о целевых объектах сеанса.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="dfd4d-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="dfd4d-169">Возвращает строку для каждого сеанса событий, относящегося к текущей базе данных.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="dfd4d-170">В Microsoft SQL Server имена аналогичных представлений каталога не содержат указание *\_database* и выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="dfd4d-171">**sys.dm_xe_sessions** вместо имени</span><span class="sxs-lookup"><span data-stu-id="dfd4d-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="dfd4d-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="dfd4d-173">Общие DMV</span><span class="sxs-lookup"><span data-stu-id="dfd4d-173">DMVs common to both</span></span>
<span data-ttu-id="dfd4d-174">Для расширенных событий существуют дополнительные DMV, которые являются общими и для Базы данных SQL Azure, и для Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="dfd4d-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="dfd4d-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="dfd4d-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="dfd4d-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="dfd4d-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="dfd4d-179">Поиск доступных расширенных событий, действий и целевых объектов</span><span class="sxs-lookup"><span data-stu-id="dfd4d-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="dfd4d-180">Для получения списка доступных событий, действий и целевых объектов можно выполнить простую SQL-команду **SELECT** .</span><span class="sxs-lookup"><span data-stu-id="dfd4d-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

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


<span data-ttu-id="dfd4d-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="dfd4d-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="dfd4d-182">Целевые объекты для сеансов событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="dfd4d-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="dfd4d-183">Результаты сеансов событий в Базе данных SQL можно фиксировать в следующих целевых объектах:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="dfd4d-184">[Целевой объект "Кольцевой буфер"](http://msdn.microsoft.com/library/ff878182.aspx) — сохраняет данные события в памяти на недолгое время.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="dfd4d-185">[Целевой объект "Счетчик событий"](http://msdn.microsoft.com/library/ff878025.aspx) — подсчитывает все события, произошедшие за время сеанса расширенных событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="dfd4d-186">[Целевой объект "Файл событий"](http://msdn.microsoft.com/library/ff878115.aspx) — записывает все буферы в контейнер хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="dfd4d-187">API [трассировки событий для Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) недоступен для расширенных событий в Базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="dfd4d-188">Ограничения</span><span class="sxs-lookup"><span data-stu-id="dfd4d-188">Restrictions</span></span>

<span data-ttu-id="dfd4d-189">В облачной среде Базы данных SQL имеется несколько отличий, связанных с обеспечением безопасности.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="dfd4d-190">Функция расширенных событий основана на изоляционной модели с одним клиентом.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="dfd4d-191">Сеанс событий в одной базе данных не может получить доступ к данным или событиям в другой базе данных.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="dfd4d-192">В контексте базы данных **master** оператор **CREATE EVENT SESSION** не вызывается.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="dfd4d-193">Модель разрешений</span><span class="sxs-lookup"><span data-stu-id="dfd4d-193">Permission model</span></span>

<span data-ttu-id="dfd4d-194">Чтобы вызвать оператор **CREATE EVENT SESSION**, требуется разрешение на **управление**.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="dfd4d-195">Владелец базы данных (dbo) имеет разрешение на **управление** .</span><span class="sxs-lookup"><span data-stu-id="dfd4d-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="dfd4d-196">Авторизации контейнера хранилища</span><span class="sxs-lookup"><span data-stu-id="dfd4d-196">Storage container authorizations</span></span>

<span data-ttu-id="dfd4d-197">Маркер SAS, сформированный для вашего контейнера хранилища Azure, должен указывать **rwl** для разрешений.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="dfd4d-198">Значение **rwl** обеспечивает следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="dfd4d-199">чтение</span><span class="sxs-lookup"><span data-stu-id="dfd4d-199">Read</span></span>
- <span data-ttu-id="dfd4d-200">запись</span><span class="sxs-lookup"><span data-stu-id="dfd4d-200">Write</span></span>
- <span data-ttu-id="dfd4d-201">список</span><span class="sxs-lookup"><span data-stu-id="dfd4d-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="dfd4d-202">Рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="dfd4d-202">Performance considerations</span></span>

<span data-ttu-id="dfd4d-203">Существуют сценарии, в которых интенсивное использование расширенных событий может задействовать больше активной памяти, чем допустимо для сохранения работоспособности всей системы.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="dfd4d-204">В связи с этим система Базы данных SQL Azure динамически устанавливает и корректирует ограничения на объем активной памяти, который может использоваться сеансом событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="dfd4d-205">Динамические расчеты выполняются с учетом множества факторов.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="dfd4d-206">При появлении сообщения о превышении максимального объема памяти можно предпринять следующие коррекционные меры:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="dfd4d-207">уменьшить количество одновременно запущенных сеансов событий;</span><span class="sxs-lookup"><span data-stu-id="dfd4d-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="dfd4d-208">уменьшить объем памяти, заданный в предложении **MAX\_MEMORY**, с помощью операторов **CREATE** и **ALTER**.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="dfd4d-209">Задержки сети</span><span class="sxs-lookup"><span data-stu-id="dfd4d-209">Network latency</span></span>

<span data-ttu-id="dfd4d-210">Целевой объект **Файл событий** может столкнуться с медленной работой или отказами сети при сохранении данных в большие двоичные объекты хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="dfd4d-211">Другие события в Базе данных SQL могут откладываться до установки подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="dfd4d-212">Такая задержка может замедлить вашу работу.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="dfd4d-213">Чтобы уменьшить этот риск, старайтесь не указывать для параметра **EVENT_RETENTION_MODE** значение **NO_EVENT_LOSS** в определениях сеанса событий.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="dfd4d-214">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="dfd4d-214">Related links</span></span>

- <span data-ttu-id="dfd4d-215">[Использование Azure PowerShell со службой хранилища Azure](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="dfd4d-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="dfd4d-216">Командлеты службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="dfd4d-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="dfd4d-217">[Использование Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md) — статья содержит полную информацию о PowerShell и службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="dfd4d-218">Использование хранилища BLOB-объектов из .NET</span><span class="sxs-lookup"><span data-stu-id="dfd4d-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="dfd4d-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="dfd4d-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="dfd4d-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="dfd4d-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="dfd4d-221">Публикации в блоге Джонтана Кехайаса (Jonathan Kehayias) о расширенных событий в Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="dfd4d-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="dfd4d-222">Веб-страница с *обновлениями службы* Azure с ограничением по параметру базы данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="dfd4d-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="dfd4d-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="dfd4d-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="dfd4d-224">Другие статьи с примерами кода для работы с расширенными событиями доступны по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="dfd4d-225">Обязательно проверяйте, предназначен ли пример для Microsoft SQL Server или для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="dfd4d-226">После этого вы сможете решить, какие поправки нужно внести в пример кода.</span><span class="sxs-lookup"><span data-stu-id="dfd4d-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
