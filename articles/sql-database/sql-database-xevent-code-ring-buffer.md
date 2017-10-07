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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>Код целевого объекта "Кольцевой буфер" для расширенных событий в базе данных SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Полный пример кода, необходимой для hello простой быстро toocapture и сообщения сведений для расширенного события во время теста. Hello простой цель для данных расширенных событий — hello [цели кольцевого буфера](http://msdn.microsoft.com/library/ff878182.aspx).

В этой статье представлен пример кода Transact-SQL, который:

1. Создает таблицу с данными toodemonstrate с.
2. Создает сеанс для имеющегося расширенного события, а именно **sqlserver.sql_statement_starting**.
   
   * Hello событие является ограниченной tooSQL инструкции, содержащие определенную строку обновления: **оператор LIKE '% tabEmployee обновления %'**.
   * Выбирает toosend hello выходных данных цели tooa hello событий типа кольцевого буфера, а именно **package0.ring_buffer**.
3. Запускает сеанс событий hello.
4. Выдает пару простых операторов SQL UPDATE.
5. Выдает SQL SELECT инструкции tooretrieve выходных данных событий из кольцевого буфера hello.
   
   * **sys.dm_xe_database_session_targets** и другие динамические административные представления (DMV) объединяются.
6. Останавливает сеанс событий hello.
7. Удаляет hello цели кольцевого буфера, toorelease свои ресурсы.
8. Удаляет сеанс событий hello и демонстрация таблицы hello.

## <a name="prerequisites"></a>Предварительные требования

* Учетная запись и подписка Azure. Вы можете зарегистрироваться, чтобы получить [бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/).
* Любая база данных, позволяющая создать таблицу.
  
  * При необходимости вы можете быстро [создать демонстрационную базу данных **AdventureWorksLT**](sql-database-get-started.md).
* SQL Server Management Studio (ssms.exe), в идеале — последняя ежемесячная версия обновления. 
  Вы можете скачать последнюю ssms.exe hello из:
  
  * Статья [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Для загрузки toohello прямую ссылку.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>Пример кода

После внесения существенных изменений hello следующий образец кода кольцевого буфера может выполняться в базе данных SQL Azure или Microsoft SQL Server. Hello отличается наличием hello hello узла «_базы данных» в имени hello некоторых динамических административных представлений (DMV), используемый в предложении FROM hello в шаге 5. Например:

* sys.dm_xe**_database**_session_targets
* sys.dm_xe_session_targets

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

## <a name="ring-buffer-contents"></a>Содержимое кольцевого буфера

Можно использовать образец кода hello toorun ssms.exe.

результаты tooview hello, что щелчок ячейки hello под заголовком столбца hello **target_data_XML**.

Затем в области результатов hello мы была нажата кнопка hello ячейку под заголовком столбца hello **target_data_XML**. Нажмите кнопку Создать другую вкладку файла в ssms.exe, в которой hello отображается содержимое ячейки hello результат, как XML.

Hello выходные данные приведены в hello после блока. Он выглядит длинным, но содержит всего два элемента **<event>** .

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


#### <a name="release-resources-held-by-your-ring-buffer"></a>Освобождение ресурсов, занятых кольцевым буфером

Закончив с вашей кольцевого буфера, можно удалить его и освобождения ресурсов выдачи **ALTER** как hello следующем:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


Hello определения сеанса событий обновления, но не удалены. Позднее можно добавить еще один экземпляр сеанса событий tooyour hello кольцевого буфера:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>Дополнительные сведения

Hello первичный раздел для расширенных событий в базе данных SQL Azure является:

* [Рекомендации по работе с расширенными событиями в Базе данных SQL](sql-database-xevent-db-diff-from-svr.md), где сравниваются аспекты расширенных событий в Базе данных SQL Azure и в Microsoft SQL Server.

Другие разделы образец кода для расширенных событий доступны по ссылкам hello. Тем не менее необходимо регулярно проверять любой образец toosee ли образец hello предназначен для Microsoft SQL Server и базы данных SQL Azure. Затем вы сможете решить, требуются ли незначительные изменения необходимые toorun образец hello.

* Пример кода для Базы данных SQL Azure: [Код целевого объекта "Файл событий" для расширенных событий в Базе данных SQL](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
