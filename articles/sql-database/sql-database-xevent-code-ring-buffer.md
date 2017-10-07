---
title: "aaaXEvent код кольцевого буфера для базы данных SQL | Документы Microsoft"
description: "Содержит пример кода Transact-SQL, который выполняется простое и быстрое с помощью hello кольцевого буфера целевого объекта в базе данных SQL Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="90ae6-103">Код целевого объекта "Кольцевой буфер" для расширенных событий в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="90ae6-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="90ae6-104">Полный пример кода, необходимой для hello простой быстро toocapture и сообщения сведений для расширенного события во время теста.</span><span class="sxs-lookup"><span data-stu-id="90ae6-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="90ae6-105">Hello простой цель для данных расширенных событий — hello [цели кольцевого буфера](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="90ae6-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="90ae6-106">В этой статье представлен пример кода Transact-SQL, который:</span><span class="sxs-lookup"><span data-stu-id="90ae6-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="90ae6-107">Создает таблицу с данными toodemonstrate с.</span><span class="sxs-lookup"><span data-stu-id="90ae6-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="90ae6-108">Создает сеанс для имеющегося расширенного события, а именно **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="90ae6-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="90ae6-109">Hello событие является ограниченной tooSQL инструкции, содержащие определенную строку обновления: **оператор LIKE '% tabEmployee обновления %'**.</span><span class="sxs-lookup"><span data-stu-id="90ae6-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="90ae6-110">Выбирает toosend hello выходных данных цели tooa hello событий типа кольцевого буфера, а именно **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="90ae6-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="90ae6-111">Запускает сеанс событий hello.</span><span class="sxs-lookup"><span data-stu-id="90ae6-111">Starts hello event session.</span></span>
4. <span data-ttu-id="90ae6-112">Выдает пару простых операторов SQL UPDATE.</span><span class="sxs-lookup"><span data-stu-id="90ae6-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="90ae6-113">Выдает SQL SELECT инструкции tooretrieve выходных данных событий из кольцевого буфера hello.</span><span class="sxs-lookup"><span data-stu-id="90ae6-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="90ae6-114">**sys.dm_xe_database_session_targets** и другие динамические административные представления (DMV) объединяются.</span><span class="sxs-lookup"><span data-stu-id="90ae6-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="90ae6-115">Останавливает сеанс событий hello.</span><span class="sxs-lookup"><span data-stu-id="90ae6-115">Stops hello event session.</span></span>
7. <span data-ttu-id="90ae6-116">Удаляет hello цели кольцевого буфера, toorelease свои ресурсы.</span><span class="sxs-lookup"><span data-stu-id="90ae6-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="90ae6-117">Удаляет сеанс событий hello и демонстрация таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="90ae6-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90ae6-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90ae6-118">Prerequisites</span></span>

* <span data-ttu-id="90ae6-119">Учетная запись и подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="90ae6-119">An Azure account and subscription.</span></span> <span data-ttu-id="90ae6-120">Вы можете зарегистрироваться, чтобы получить [бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90ae6-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="90ae6-121">Любая база данных, позволяющая создать таблицу.</span><span class="sxs-lookup"><span data-stu-id="90ae6-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="90ae6-122">При необходимости вы можете быстро [создать демонстрационную базу данных **AdventureWorksLT**](sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="90ae6-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="90ae6-123">SQL Server Management Studio (ssms.exe), в идеале — последняя ежемесячная версия обновления.</span><span class="sxs-lookup"><span data-stu-id="90ae6-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="90ae6-124">Вы можете скачать последнюю ssms.exe hello из:</span><span class="sxs-lookup"><span data-stu-id="90ae6-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="90ae6-125">Статья [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="90ae6-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="90ae6-126">Для загрузки toohello прямую ссылку.</span><span class="sxs-lookup"><span data-stu-id="90ae6-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="90ae6-127">Пример кода</span><span class="sxs-lookup"><span data-stu-id="90ae6-127">Code sample</span></span>

<span data-ttu-id="90ae6-128">После внесения существенных изменений hello следующий образец кода кольцевого буфера может выполняться в базе данных SQL Azure или Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="90ae6-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="90ae6-129">Hello отличается наличием hello hello узла «_базы данных» в имени hello некоторых динамических административных представлений (DMV), используемый в предложении FROM hello в шаге 5.</span><span class="sxs-lookup"><span data-stu-id="90ae6-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="90ae6-130">Например:</span><span class="sxs-lookup"><span data-stu-id="90ae6-130">For example:</span></span>

* <span data-ttu-id="90ae6-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="90ae6-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="90ae6-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="90ae6-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="90ae6-133">Содержимое кольцевого буфера</span><span class="sxs-lookup"><span data-stu-id="90ae6-133">Ring Buffer contents</span></span>

<span data-ttu-id="90ae6-134">Можно использовать образец кода hello toorun ssms.exe.</span><span class="sxs-lookup"><span data-stu-id="90ae6-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="90ae6-135">результаты tooview hello, что щелчок ячейки hello под заголовком столбца hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="90ae6-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="90ae6-136">Затем в области результатов hello мы была нажата кнопка hello ячейку под заголовком столбца hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="90ae6-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="90ae6-137">Нажмите кнопку Создать другую вкладку файла в ssms.exe, в которой hello отображается содержимое ячейки hello результат, как XML.</span><span class="sxs-lookup"><span data-stu-id="90ae6-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="90ae6-138">Hello выходные данные приведены в hello после блока.</span><span class="sxs-lookup"><span data-stu-id="90ae6-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="90ae6-139">Он выглядит длинным, но содержит всего два элемента **<event>** .</span><span class="sxs-lookup"><span data-stu-id="90ae6-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="90ae6-140">Освобождение ресурсов, занятых кольцевым буфером</span><span class="sxs-lookup"><span data-stu-id="90ae6-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="90ae6-141">Закончив с вашей кольцевого буфера, можно удалить его и освобождения ресурсов выдачи **ALTER** как hello следующем:</span><span class="sxs-lookup"><span data-stu-id="90ae6-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="90ae6-142">Hello определения сеанса событий обновления, но не удалены.</span><span class="sxs-lookup"><span data-stu-id="90ae6-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="90ae6-143">Позднее можно добавить еще один экземпляр сеанса событий tooyour hello кольцевого буфера:</span><span class="sxs-lookup"><span data-stu-id="90ae6-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="90ae6-144">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="90ae6-144">More information</span></span>

<span data-ttu-id="90ae6-145">Hello первичный раздел для расширенных событий в базе данных SQL Azure является:</span><span class="sxs-lookup"><span data-stu-id="90ae6-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="90ae6-146">[Рекомендации по работе с расширенными событиями в Базе данных SQL](sql-database-xevent-db-diff-from-svr.md), где сравниваются аспекты расширенных событий в Базе данных SQL Azure и в Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="90ae6-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="90ae6-147">Другие разделы образец кода для расширенных событий доступны по ссылкам hello.</span><span class="sxs-lookup"><span data-stu-id="90ae6-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="90ae6-148">Тем не менее необходимо регулярно проверять любой образец toosee ли образец hello предназначен для Microsoft SQL Server и базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="90ae6-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="90ae6-149">Затем вы сможете решить, требуются ли незначительные изменения необходимые toorun образец hello.</span><span class="sxs-lookup"><span data-stu-id="90ae6-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="90ae6-150">Пример кода для Базы данных SQL Azure: [Код целевого объекта "Файл событий" для расширенных событий в Базе данных SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="90ae6-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
