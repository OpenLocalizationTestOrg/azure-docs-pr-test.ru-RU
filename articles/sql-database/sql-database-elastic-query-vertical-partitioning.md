---
title: "aaaQuery в облаке баз данных с разными схемами | Документы Microsoft"
description: "как tooset копирование межбазовые запросы по вертикальной секции"
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
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)
![Запросы между таблицами в разных базах данных][1]

Базы данных с вертикальным секционированием используют разные наборы таблиц в разных базах данных. Это означает, что в этой схеме hello отличается на разных базах данных. Например, все таблицы, связанные с данными инвентаризации, хранятся в одной базе данных, а таблицы, связанные с учетом, — в другой. 

## <a name="prerequisites"></a>Предварительные требования
* Hello пользователь должен обладать разрешением ALTER ANY EXTERNAL DATA SOURCE. Это разрешение входит в состав hello разрешение ALTER DATABASE.
* Разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые toorefer toohello базового источника данных.

## <a name="overview"></a>Обзор

> [!NOTE]
> В отличие от с горизонтального секционирования этих инструкций DDL не полагаться на определение уровня данных с карты сегментов через клиентскую библиотеку hello эластичной базы данных.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Создание главного ключа и учетных данных для конкретной базы данных
Hello учетных данных используется hello эластичной запроса tooconnect tooyour удаленных баз данных.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Убедитесь, что hello `<username>` не должно содержать **»@servername»** суффикс. 
>

## <a name="create-external-data-sources"></a>Создание внешних источников данных
Синтаксис:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> необходимо задать параметр ТИПА Hello слишком**реляционной СУБД**. 
>

### <a name="example"></a>Пример
Hello следующий пример иллюстрирует использование hello hello инструкции CREATE для внешних источников данных. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

Список hello tooretrieve текущего внешних источников данных: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Внешние таблицы
Синтаксис:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Пример
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

Привет, в следующем примере показано, как tooretrieve hello список внешних таблиц из текущей базы данных hello: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Примечания
Эластичный запрос расширяет hello существующей внешней таблицы синтаксис toodefine внешних таблиц, использующих внешним источникам данных типа реляционной СУБД. Определение внешней таблицы для вертикального секционирования рассматриваются следующие аспекты hello: 

* **Схемы**: hello внешней таблицы DDL определяет схему, можно использовать в запросах. Hello схемы, предоставленных в определении внешней таблицы должен toomatch hello схемы таблиц hello в hello удаленной базы данных, где хранится hello фактические данные. 
* **Ссылка на удаленную базу данных**: hello внешней таблицы DDL ссылается tooan внешнего источника данных. Hello внешнего источника данных указывает имя логического сервера hello и имя базы данных hello удаленной базы данных, где хранятся данные таблицы фактических hello. 

С помощью внешнего источника данных, как показано в предыдущем разделе hello, hello синтаксис toocreate внешних таблиц выглядит следующим образом: 

предложение источник_данных Hello определяет hello внешнего источника данных (т. е. hello удаленной базы данных в случае вертикальное секционирование), используемый для hello внешней таблицы.  

предложения SCHEMA_NAME и OBJECT_NAME Hello содержат hello возможность toomap hello внешней таблицы определение tooa таблицы в другую схему hello удаленной базы данных или таблицы tooa с другим именем, соответственно. Это полезно, если требуется toodefine представление каталога tooa внешней таблицы или динамического административного Представления в удаленной базе данных - или другая ситуация, где имя удаленной таблицы hello уже занято локально.  

Hello следующая инструкция DDL удаляет существующее определение внешней таблицы из локального каталога hello. Он не влияет на hello удаленной базы данных. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Разрешения для ВНЕШНЕЙ таблицы в инструкции CREATE, DROP**: для внешней таблицы DDL, который также требуется toorefer toohello базового источника данных, необходимы разрешения ALTER ANY EXTERNAL DATA SOURCE.  

## <a name="security-considerations"></a>Вопросы безопасности
Пользователи с доступом toohello внешней таблицы автоматически получают доступ toohello удаленные базовые таблицы под hello учетных данных, заданный в определении источника внешних данных hello. Следует тщательно управлять доступом toohello внешней таблицы в порядке tooavoid нежелательные повышение привилегий через hello учетных данных источника внешних данных hello. Регулярные разрешения SQL может быть используется tooGRANT или REVOKE доступа tooan внешней таблицы, как если бы он был обычной таблицы.  

## <a name="example-querying-vertically-partitioned-databases"></a>Пример: запрос баз данных с вертикальным секционированием
Hello следующий запрос выполняет Тройное соединение между hello двух локальных таблиц заказов и порядок строк и hello удаленной таблицы для клиентов. Ниже приведен пример hello ссылку данных сценария для эластичного запроса: 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Хранимая процедура для удаленного выполнения T-SQL: sp\_execute_remote
Эластичный запроса также представляет хранимую процедуру, которая обеспечивает прямой доступ toohello сегментов. Hello вызывается хранимая процедура [sp\_выполнение \_удаленного](https://msdn.microsoft.com/library/mt703714) и может быть используется tooexecute удаленных хранимых процедур или код T-SQL на hello удаленных баз данных. Он принимает hello следующие параметры: 

* Имя источника данных (nvarchar): имя hello hello внешнего источника данных типа реляционной СУБД. 
* Запрос (nvarchar): hello T-SQL запрос toobe выполнена на каждый сегмент. 
* Объявление параметра (nvarchar) - необязательно: строка, в которой определения типов данных для параметров hello в качестве параметра запроса hello (например sp_executesql). 
* Список значений параметров (необязательно): разделенный запятыми список значений параметров (например, sp_executesql).

Hello sp\_выполнение\_удаленного использует hello внешнего источника данных в hello параметров вызова tooexecute hello, вводимых в удаленных базах данных hello инструкции T-SQL. Она использует учетные данные hello hello внешних данных tooconnect toohello shardmap диспетчера базы данных-источника и hello удаленных баз данных.  

Пример: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a>Подключение для инструментов
Можно использовать регулярные tooconnect строки подключения SQL Server восстановления toodatabases средств интеграции бизнес-Аналитики и данных на сервере баз данных SQL Server hello эластичной запросов включена и внешних таблиц, определенных. Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server. Затем можно ссылаться toohello эластичной запрос к базе данных и ее внешней таблицы, так же, как и другие базы данных SQL Server, что для подключения toowith средством. 

## <a name="best-practices"></a>Рекомендации
* Убедитесь, что в этой базе данных hello эластичной запроса конечной точки задано удаленной базы данных toohello доступ путем разрешения доступа для служб Azure в конфигурации брандмауэра баз данных SQL Server. Эти учетные данные hello также убедиться, указанное во внешних данных hello определение источника успешно входят в удаленной базе данных hello и имеет hello разрешения tooaccess hello удаленной таблицы.  
* Эластичный запроса оптимально подходит для запросов где большинство hello вычисление может выполняться на hello удаленных баз данных. Как правило, получается hello наилучшую производительность запросов с предикатами Выборочный фильтров, которые могут быть обработаны на hello удаленных баз данных или соединения, которые могут быть полностью выполнены hello удаленную базу данных. Другие шаблоны запросов может потребоваться tooload большие объемы данных из удаленной базы данных hello и может наблюдаться снижение производительности. 

## <a name="next-steps"></a>Дальнейшие действия

* Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).
* Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).
* Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).
* Описание синтаксиса и примеры запросов горизонтально секционированных данных см. в разделе [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-horizontal-partitioning.md).
* В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
