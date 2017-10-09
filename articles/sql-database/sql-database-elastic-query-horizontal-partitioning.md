---
title: "aaaReporting между базами данных с горизонтальным масштабированием облачных | Документы Microsoft"
description: "как tooset копирование эластичной запросов за горизонтальных секций"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Отчеты по масштабируемым облачным базам данных (предварительная версия)
![Запрос по сегментам][1]

Сегментированные базы данных распределяют строки по масштабируемому уровню данных. Hello схемы похоже на все участвующие базы данных, также известные как горизонтальное секционирование. Используя эластичный запрос, можно создавать отчеты, охватывающие все базы данных в сегментированной базе данных.

Чтобы быстро приступить к работе, ознакомьтесь со статьей [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).

Сведения для несегментированных баз данных см. в статье [Запрос к нескольким облачным базам данных с разными схемами](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Предварительные требования
* Создание карты сегментов с помощью клиентской библиотеки hello эластичной базы данных. Ознакомьтесь с [управлением картами сегментов](sql-database-elastic-scale-shard-map-management.md). Или использовать пример приложения hello [начало работы с инструментами эластичной базы данных](sql-database-elastic-scale-get-started.md).
* Кроме того, в разделе [миграции существующей базы данных вне tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).
* Hello пользователь должен обладать разрешением ALTER ANY EXTERNAL DATA SOURCE. Это разрешение входит в состав hello разрешение ALTER DATABASE.
* Разрешения ALTER ANY EXTERNAL DATA SOURCE, необходимые toorefer toohello базового источника данных.

## <a name="overview"></a>Обзор
Эти инструкции создания представления метаданных hello уровень сегментированных данных в hello эластичной запрос к базе данных. 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1. Создание главного ключа и учетных данных для конкретной базы данных
Hello учетных данных используется hello эластичной запроса tooconnect tooyour удаленных баз данных.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Убедитесь в том, что hello *»\<username\>»* не должно содержать *»@servername»* суффикс. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2. Создание внешних источников данных
Синтаксис:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Пример
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Получение списка hello текущего внешних источников данных: 

    select * from sys.external_data_sources; 

Hello внешний источник данных ссылается на карте сегментов. Запрос эластичной затем использует hello внешнего источника данных и базовой сегментов карты tooenumerate hello баз данных, которые участвуют в уровень данных hello hello. Hello же учетные данные, используемые tooread карта сегментов hello и tooaccess hello данные на сегменты hello во время обработки hello эластичной запроса. 

## <a name="13-create-external-tables"></a>1.3. Создание внешних таблиц
Синтаксис:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Пример**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Получить список hello внешние таблицы из текущей базы данных hello: 

    SELECT * from sys.external_tables; 

toodrop внешних таблиц:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Примечания
Hello данных\_предложение источника определяет hello внешнего источника данных (карта сегментов), используемый для hello внешней таблицы.  

Hello СХЕМЫ\_имя и объект\_предложений имя сопоставления hello таблица tooa определения внешней таблицы в другую схему. Если не указано, hello схему удаленного объекта hello полагается toobe «dbo» а его имя является определяемое имя внешней таблицы идентичные toohello toobe. Это полезно, если hello имя удаленной таблицы уже используется в базе данных hello место toocreate hello внешней таблицы. Например требуется toodefine внешней таблицы tooget статистического представления представлений каталога или динамических административных представлений с горизонтальным масштабированием данными уровня. Поскольку представления каталогов и динамические административные представления уже существует локально, не может использовать их имена для определения hello внешней таблицы. Вместо этого используйте другое имя и используйте представление каталога hello или hello имя динамические административные Представления в СХЕМЕ hello\_имя и (или) ОБЪЕКТА\_имя предложения. (См. пример hello). 

предложение РАСПРОСТРАНЕНИЯ Hello указывает hello распределение данных, используемого для этой таблицы. Hello обработчик запросов использует сведения hello в hello РАСПРОСТРАНЕНИЯ предложение toobuild hello наиболее эффективный планов запросов.  

1. **СЕГМЕНТИРОВАННЫХ** означает данные секционируются горизонтально hello базах данных. ключ разделов для распределения данных hello hello Hello **< sharding_column_name >** параметра.
2. **РЕПЛИКАЦИЯ** означает, что одинаковых копий hello таблицы присутствуют в каждой базе данных. Это ваш tooensure ответственность, что реплик hello идентичны для всех баз данных hello.
3. **ROUND\_ПЕРЕБОРОМ** означает, что hello таблица секционирована по горизонтали с помощью метода распространения зависит от приложения. 

**Ссылка на уровень данных**: hello внешней таблицы DDL ссылается tooan внешнего источника данных. Hello внешнего источника данных указывает карта сегментов, предоставляющий hello внешней таблицы toolocate необходимые сведения hello всех hello базах данных уровня данных. 

### <a name="security-considerations"></a>Вопросы безопасности
Пользователи с доступом toohello внешней таблицы автоматически получают доступ toohello удаленные базовые таблицы под hello учетных данных, заданный в определении источника внешних данных hello. Избегайте нежелательных повышение привилегий через учетных данных hello hello внешнего источника данных. Методы GRANT или REVOKE применяются к внешней таблице так же, как и к обычной.  

Определив внешний источник данных и внешние таблицы, вы можете использовать все возможности T-SQL для создания запросов к внешним таблицам.

## <a name="example-querying-horizontal-partitioned-databases"></a>Пример: запрос баз данных с горизонтальным секционированием
Hello следующий запрос выполняет Тройное соединение между хранилищами, заказов и строк заказов и использует несколько статистических выражений и выборочной фильтра. Предполагается, что (1) горизонтальных секционирования (сегментов) и (2) порядок строк, заказов и хранилищ сегментированных по столбцу идентификатора hello хранилища, и hello эластичной запроса можно выравнивать hello соединения на сегменты hello и обрабатывать hello ресурсоемким hello запроса hello сегменты в параллельном режиме. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

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
Использовать регулярные tooconnect строки подключения SQL Server приложения, бизнес-Аналитики и данных интеграции средств toohello базы данных с определениях внешней таблицы. Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server. Ссылаться на базу данных hello эластичной запросов, как и любой другой SQL Server базы данных, соединение toohello инструмент и использовать внешние таблицы из средства или приложения, как если бы они были локальными таблицами. 

## <a name="best-practices"></a>Рекомендации
* Убедитесь, что для этой базы данных hello эластичной запроса конечной точки предоставлен доступ к базе данных shardmap toohello и все сегменты через брандмауэры SQL DB приветствия.  
* Проверяет, или применять hello распределение данных, определяемый hello внешней таблицы. При распространении фактических данных отличается от распространения hello, указанный в определении таблицы, запросы, может привести к непредвиденным результатам. 
* Эластичный запрос в настоящее время не выполняет сегментов исключения при предикаты для ключа сегментирования hello позволяющих toosafely исключения определенных сегментов из обработки.
* Эластичный запроса лучше всего работает для запросов, где большинство hello вычисление может выполняться на сегменты hello. Как правило, получается hello наилучшую производительность запросов с предикатами Выборочный фильтров, которые можно оценить на сегменты hello или соединения через hello секционирование ключи, которые могут выполняться в виде выровненные по секциям на всех сегментах. Другие шаблоны запросов, может потребоваться tooload большие объемы данных из головного узла hello сегментов toohello и может наблюдаться снижение производительности

## <a name="next-steps"></a>Дальнейшие действия

* Общие сведения об эластичных запросах см. в разделе [Обзор эластичных запросов к базе данных SQL Azure (предварительная версия)](sql-database-elastic-query-overview.md).
* Руководств по вертикальному секционированию см. в статье [Приступая к работе с межбазовыми запросами (вертикальное секционирование) (предварительная версия)](sql-database-elastic-query-getting-started-vertical.md).
* Описание синтаксиса и примеры запросов вертикально секционированных данных см. в разделе [Запрос к нескольким облачным базам данных с разными схемами (предварительная версия)](sql-database-elastic-query-vertical-partitioning.md).
* Руководство по горизонтальному секционированию (сегментированию) см. в статье [Отчеты по масштабируемым облачным базам данных (предварительная версия)](sql-database-elastic-query-getting-started.md).
* В описании [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) приведена хранимая процедура, которая выполняет инструкцию Transact-SQL для отдельной удаленной базы данных SQL Azure или набора баз данных, выступающих в качестве сегментов в схеме горизонтального секционирования.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
