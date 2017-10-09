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
# <a name="extended-events-in-sql-database"></a>Расширенные события в Базе данных SQL
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Этот разделе объясняется, как реализация hello расширенных событий в базе данных SQL Azure немного отличается сравниваемых tooextended событий в Microsoft SQL Server.

- Базы данных SQL V12 приобретенные функции hello расширенных событий в hello второй половине календаря 2015.
- SQL Server включает расширенные события с 2008 года.
- набор функций Hello расширенных событий в базе данных SQL является надежным подмножество функций hello на сервере SQL Server.

*XEvents* — это неофициальное обозначение расширенных событий, которое встречается в блоках и других неофициальных источниках.

Дополнительные сведения о расширенных событиях для базы данных SQL Azure и Microsoft SQL Server доступны в следующих разделах.

- [Quick Start: Extended events in SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Расширенные события](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Предварительные требования

В данной статье предполагается, чтобы вы уже ознакомились со следующими компонентами:

- [Служба Базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/);
- [Расширенные события](http://msdn.microsoft.com/library/bb630282.aspx) в Microsoft SQL Server.

- Hello большая часть документации о расширенных событий применяется tooboth SQL Server и базы данных SQL.

Предыдущий раскрытия toohello следующих элементов полезно при выборе файла событий как hello hello [целевой](#AzureXEventsTargets):

- [Служба хранилища Azure](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [С помощью Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md) -предоставляет подробные сведения о службе хранилища Azure hello и PowerShell.

## <a name="code-samples"></a>Примеры кода

Связанные разделы содержат два примера кода.


- [Код целевого объекта "Кольцевой буфер" для расширенных событий в Базе данных SQL](sql-database-xevent-code-ring-buffer.md)
    - Простой короткий сценарий Transact-SQL.
    - Мы подчеркнуть hello кода образца раздела, что после завершения целевой кольцевой буфер должен освободить ресурсы, его, выполнив перетаскивания alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` инструкции. Впоследствии вы сможете добавить другой экземпляр кольцевого буфера с помощью оператора `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Код целевого объекта "Файл событий" для расширенных событий в Базе данных SQL](sql-database-xevent-code-event-file.md)
    - Этап 1 — PowerShell toocreate контейнер службы хранилища Azure.
    - Этап 2 — Transact-SQL, использующего hello контейнер хранилища Azure.

## <a name="transact-sql-differences"></a>Отличия Transact-SQL


- При выполнении hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) команды на сервере SQL Server использовать hello **ON SERVER** предложения. Но в базе данных SQL используйте hello **ON DATABASE** предложение вместо него.


- Hello **ON DATABASE** предложение также применяется toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) и [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) команд Transact-SQL.


- Лучший способ — это параметр сеанса событий tooinclude hello объекта **STARTUP_STATE = ON** в ваш **CREATE EVENT SESSION** или **ALTER EVENT SESSION** инструкции.
    - Hello **= ON** значение поддерживает автоматический перезапуск после перенастройки hello логическую базу данных из-за tooa перехода на другой ресурс.

## <a name="new-catalog-views"></a>Новые представления каталога

Hello расширенных событий поддерживается несколько [представления каталога](http://msdn.microsoft.com/library/ms174365.aspx). Представления каталога сообщают об *метаданных и определений* сеансов событий, созданных пользователем в текущей базе данных hello. представления Hello не возвращают сведения об экземплярах сеансов активных событий.

| Имя<br/>представления каталога | Описание |
|:--- |:--- |
| **sys.database_event_session_actions** |Возвращает строку для каждого действия с каждым событием в сеансе событий. |
| **sys.database_event_session_events** |Возвращает строку для каждого события в сеансе событий. |
| **sys.database_event_session_fields** |Возвращает строку для каждого настраиваемого столбца, который можно прямо задавать для событий и целевых объектов. |
| **sys.database_event_session_targets** |Возвращает строку для каждого целевого объекта события в сеансе событий. |
| **sys.database_event_sessions** |Возвращает строку для каждого сеанса событий в базе данных hello базы данных SQL. |

В Microsoft SQL Server аналогичные представления каталогов имеют имена, содержащие *.server\_* вместо *.database\_*. шаблон имени Hello аналогичен **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>Новые динамические административные представления [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)

База данных SQL Azure включает [динамические административные представления (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) , которые поддерживают расширенные события. DMV сообщают об *активных* сеансах событий.

| Имя DMV | Описание |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Возвращает сведения о действиях в сеансе событий. |
| **sys.dm_xe_database_session_events** |Возвращает сведения о событиях в сеансе. |
| **sys.dm_xe_database_session_object_columns** |Отображает значения конфигурации hello объекты, которые являются tooa связанного сеанса. |
| **sys.dm_xe_database_session_targets** |Возвращает сведения о целевых объектах сеанса. |
| **sys.dm_xe_database_sessions** |Возвращает по строке для каждого сеанса событий, является toohello области текущей базы данных. |

В Microsoft SQL Server, аналогичные представления каталога с именем без hello  *\_базы данных* часть hello имя, такое как:

- **sys.dm_xe_sessions** вместо имени<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Общие tooboth динамических административных представлений
Для расширенных событий существуют дополнительные динамические административные представления, общие tooboth базы данных SQL Azure и Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Найти hello доступных расширенных событий, действия и целевые объекты

Можно выполнить простые SQL **ВЫБЕРИТЕ** tooobtain список доступных событий hello, действия и целевой объект.

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


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Целевые объекты для сеансов событий в Базе данных SQL

Результаты сеансов событий в Базе данных SQL можно фиксировать в следующих целевых объектах:

- [Целевой объект "Кольцевой буфер"](http://msdn.microsoft.com/library/ff878182.aspx) — сохраняет данные события в памяти на недолгое время.
- [Целевой объект "Счетчик событий"](http://msdn.microsoft.com/library/ff878025.aspx) — подсчитывает все события, произошедшие за время сеанса расширенных событий.
- [Целевого файла событий](http://msdn.microsoft.com/library/ff878115.aspx) -контейнер хранилища Azure tooan запись всех буферов.

Hello [трассировки событий для Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API недоступен для расширенных событий в базе данных SQL.

## <a name="restrictions"></a>Ограничения

Существует несколько различий, связанных с безопасностью befitting hello облачной среде базы данных SQL:

- Расширенные события основанная на hello модель изоляции одного клиента. Сеанс событий в одной базе данных не может получить доступ к данным или событиям в другой базе данных.
- Не удается выпустить **CREATE EVENT SESSION** инструкции в контексте hello hello **master** базы данных.

## <a name="permission-model"></a>Модель разрешений

Необходимо иметь **управления** разрешений на базу данных tooissue hello **CREATE EVENT SESSION** инструкции. Hello владельца базы данных (dbo) имеет **управления** разрешение.

### <a name="storage-container-authorizations"></a>Авторизации контейнера хранилища

можно создавать для контейнера хранилища Azure необходимо указать имя маркера SAS Hello **rwl** для разрешения hello. Hello **rwl** значение обеспечивает hello следующие разрешения:

- чтение
- запись
- список

## <a name="performance-considerations"></a>Рекомендации по производительности

Существуют сценарии, где интенсивное использование расширенных событий могут накапливаться более активной памяти, не находится в работоспособном состоянии для hello системы в целом. Таким образом hello системы базы данных SQL Azure динамически устанавливает и настраивает ограничения на объем hello активной памяти, которая суммируется сеанс событий. Многие факторы углубляться динамическое вычисление hello.

При появлении сообщения о превышении максимального объема памяти можно предпринять следующие коррекционные меры:

- уменьшить количество одновременно запущенных сеансов событий;
- Через ваш **создать** и **ALTER** инструкции для сеансов событий уменьшения hello объема памяти, укажите на hello **MAX\_памяти** предложения.

### <a name="network-latency"></a>Задержки сети

Hello **файла событий** целевой могут возникать задержки в сети или сбои во время сохранения tooAzure данных хранилища больших двоичных объектов. Другие события в базе данных SQL может быть отложен ожидании toocomplete связи сети hello. Такая задержка может замедлить вашу работу.

- toomitigate производительности этот риск, не задавайте hello **EVENT_RETENTION_MODE** параметр слишком**NO_EVENT_LOSS** в определениях сеанса событий.

## <a name="related-links"></a>Связанные ссылки

- [Использование Azure PowerShell со службой хранилища Azure](../storage/common/storage-powershell-guide-full.md)
- [Командлеты службы хранилища Azure](http://msdn.microsoft.com/library/dn806401.aspx)
- [С помощью Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md) -предоставляет подробные сведения о службе хранилища Azure hello и PowerShell.
- [Как toouse хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREATE EVENT SESSION (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Публикации в блоге Джонтана Кехайаса (Jonathan Kehayias) о расширенных событий в Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Hello Azure *обновления службы* веб-страницы, сужена tooAzure параметр базы данных SQL:
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


Другие разделы образец кода для расширенных событий доступны по ссылкам hello. Тем не менее необходимо регулярно проверять любой образец toosee ли образец hello предназначен для Microsoft SQL Server и базы данных SQL Azure. Затем вы сможете решить, требуются ли незначительные изменения необходимые toorun образец hello.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
