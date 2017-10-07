---
title: "aaaMonitoring производительность базы данных в базе данных SQL Azure | Документы Microsoft"
description: "Сведения о способах hello мониторинг с помощью средств Azure и динамические административные представления базы данных."
keywords: "мониторинг базы данных, производительность облачной базы данных"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Мониторинг производительности базы данных в базе данных SQL Azure
Наблюдение за производительностью hello базы данных SQL в Azure начинается с наблюдения за hello ресурсов относительный toohello уровень использования производительности базы данных, которая выбирается. Мониторинг помогает определить емкостью лишние или возникли проблемы, так как израсходован ресурсы базы данных, и затем решить, будет ли уровень производительности времени tooadjust hello и [уровень обслуживания](sql-database-service-tiers.md) базы данных. Можно отслеживать с помощью графических средств в hello базы данных [портал Azure](https://portal.azure.com) или при помощи SQL [динамические административные представления](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Мониторинг баз данных с помощью портала Azure hello
В hello [портал Azure](https://portal.azure.com/), можно наблюдать за одной базы данных, выбрав эту базу данных и выберите пункт hello **мониторинг** диаграммы. Откроется окно **метрика** окно, в котором можно изменить, щелкнув hello **изменение диаграммы** кнопки. Добавьте hello следующие метрики:

* Процент использования ЦП
* Процент использования DTU
* Процент операций ввода/вывода данных
* Размер базы данных в процентах

После добавления этих метрик, вы можете продолжить tooview их в hello **мониторинг** диаграмму, содержащую Дополнительные сведения о hello **метрика** окна. Все четыре метрики показывают hello среднее использование процент относительного toohello **DTU** базы данных. В разделе hello [уровней служб](sql-database-service-tiers.md) статьи приведены сведения о Dtu.

![Мониторинг производительности базы данных для разных уровней служб.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

Также можно настроить предупреждения по метрикам производительности hello. Нажмите кнопку hello **добавить оповещение** кнопку в hello **метрика** окна. Выполните мастер tooconfigure hello оповещения. У вас есть параметр tooalert hello метрики hello превышает определенный порог или hello метрика выходит за пределы определенного порогового значения.

Например если предполагается hello рабочей нагрузки на toogrow вашей базы данных, вы можете tooconfigure оповещение по электронной почте каждый раз, когда базы данных достигает 80% на любой из метрик производительности hello. Это можно использовать как раннее toofigure предупреждение, когда может потребоваться tooswitch toohello следующий уровень производительности.

метрики производительности Hello также помогают определить, при наличии возможности toodowngrade tooa низкой производительностью. Предположим, вы используете базы данных Standard S2 и демонстрируют метрики производительности, в среднем hello базы данных не использует более чем 10% в любой момент времени. Вполне вероятно, hello базы данных будут нормально работать Standard S1. Однако иметь в виду рабочих нагрузок, перед внесением hello решение toomove tooa низкий уровень производительности Резкие скачки и изменения.

## <a name="monitor-databases-using-dmvs"></a>Мониторинг баз данных с помощью динамических административных представлений
Hello же метрики, предоставляемые в портале hello, также доступны через системные представления: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) в логической hello **master** базы данных вашего сервера и [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) в базе данных пользователей hello. Используйте **sys.resource_stats** при необходимости toomonitor менее подробных данных в течение длительного периода времени. Используйте **sys.dm_db_resource_stats** при необходимости toomonitor более подробных данных в течение меньшего времени. Дополнительные сведения см. в статье [База данных SQL Azure и производительность отдельных баз данных](sql-database-single-database-monitor.md#monitor-resource-use).

> [!NOTE]
> При использовании в базах данных устаревших выпусков Web Edition и Business Edition **sys.dm_db_resource_stats** возвращает пустой результирующий набор.
>
>

### <a name="monitor-resource-use"></a>Отслеживание использования ресурсов

Использование ресурсов можно отслеживать с помощью [анализа производительности запросов базы данных SQL](sql-database-query-performance.md) и [хранилища запросов](https://msdn.microsoft.com/library/dn817826.aspx).

Кроме того, для отслеживания использования можно применять два приведенных ниже представления.

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Можно использовать hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) представление в каждой базе данных SQL. Hello **sys.dm_db_resource_stats** представлении отображаются последние ресурсов уровня обслуживания относительный toohello использования данных. Средний процент нагрузки ЦП, показатели операций ввода-вывода данных, записи в журнал и данные о памяти записываются каждые 15 секунд и хранятся 1 час.

Так как это представление содержит более подробные сведения об использовании ресурсов, сначала используйте представление **sys.dm_db_resource_stats** для любого анализа текущего состояния и устранения неполадок. Например этот запрос показаны hello среднее и максимальное ресурсов используют для текущей базы данных hello по hello последний час:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Для других запросов см. Примеры hello в [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) представления в hello **master** база данных содержит дополнительные сведения, которые можно отслеживать производительность hello базы данных SQL на уровне по производительности и уровня определенной службы . Hello данные собираются каждые 5 минут и сохраняется для около 35 дней. Это представление полезно для анализа использования ресурсов Базы данных SQL за более долгий период.

Hello следующей диаграмме показано использование ресурсов ЦП hello для расширенной базы данных с уровнем производительности P2 hello за каждый час в течение недели. На этом графике начинается в понедельник, показывает 5 рабочих дней, а затем показывает выходным, когда происходит гораздо меньшего приложения hello.

![Использование ресурсов Базы данных SQL](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

На основе данных hello этой базы данных в настоящее время имеет Пиковая нагрузка ЦП чуть более 50 процентов ЦП использовать уровень производительности относительный toohello P2 (полдень вторника). Если ЦП hello главным фактором ресурсного профиля приложения hello, может решить, что P2 — hello правой универсальное tooguarantee уровня производительности, который всегда hello рабочей нагрузки. Если предполагается, что приложение toogrow со временем, это toohave рекомендуется увеличить буфер ресурсов, чтобы приложение hello не никогда не достигнет лимита уровня производительности hello. При увеличении уровня производительности hello может помочь избежать заметных ошибок, которые могут возникнуть при базы данных не имеет достаточно power tooprocess запросов по сути, особенно в средах с задержками. Например, базы данных, которая поддерживает приложения, создающего веб-страниц на основе результатов hello вызовов базы данных.

Другие приложения могут интерпретировать hello же graph по-разному. Например если приложение пытается данные о заработной плате tooprocess каждый день и имеет hello одной диаграмме, в этом kind модели «задание» может сделать детально на уровне производительности P1. Hello уровнем производительности P1 предоставляет 100 Dtu too200 Dtu по сравнению с уровнем производительности P2 hello. Hello уровнем производительности P1 предоставляет половину производительность hello hello уровнем производительности P2. Таким образом, 50 процентов использования ЦП на уровне P2 равняется 100 процентам использования ЦП на уровне P1. Если приложение hello не имеет значения времени ожидания, может не важно, если задание занимает 2 часа или toofinish 2,5 часа, если оно закончилось сегодня. Приложение такой категории может использовать уровень Р1. Можно воспользоваться преимуществами hello тем, что периоды времени, в течение дня hello, когда ниже, использование ресурсов, чтобы все «больших (пик)» может быть перенесена в одну Пиковая hello позже в день hello. Hello уровень производительности Р1 может быть хорошо подходит для такого рода приложения (и деньги), при условии, что hello заданий можно вовремя каждый день.

Azure предоставляет доступ к базе данных SQL сведения об использовании ресурсов для каждой активной базы данных в hello **sys.resource_stats** представление hello **master** базы данных на каждом сервере. Hello в таблице hello собраны для 5-минутные интервалы. Уровней обслуживания по hello Basic, Standard и Premium hello данных может занять более 5 минут tooappear в таблице hello, поэтому эти данные лучше подходит для исторического анализа, а не analysis рядом реального времени. Запрос hello **sys.resource_stats** представление toosee hello в журнале последние данные из базы данных и toovalidate ли резервирование hello выбраны доставляется hello производительности при необходимости.

> [!NOTE]
> Должен быть подключенным toohello **master** базы данных из вашего tooquery логический сервер базы данных SQL **sys.resource_stats** в следующих примерах hello.
> 
> 

В этом примере показано, как представляется hello данные в этом представлении:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![представление каталога sys.resource_stats Hello](./media/sql-database-performance-guidance/sys_resource_stats.png)

Hello Приведем пример можно различными способами, которые можно использовать hello **sys.resource_stats** представление tooget сведения об использовании ресурсов в базе данных SQL из каталога:

1. toolook на hello за неделю ресурсов используйте для базы данных userdb1 hello, можно выполнить этот запрос:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. tooevaluate насколько hello уровень производительности подходит для рабочей нагрузки, необходимо toodrill вниз в каждый аспект метрики ресурсов hello: ЦП, операций чтения, записи, количество рабочих потоков и число сеансов. Ниже приводится измененный запрос с использованием **sys.resource_stats** tooreport Здравствуйте, среднее и максимальное значения эти метрики ресурсов:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. По этой информации о hello среднее и максимальное значения по каждому ресурсу можно оценить, насколько хорошо рабочей нагрузки попадают hello выбранный уровень производительности. Как правило, средние значения из **sys.resource_stats** предоставляют хорошую основу toouse hello целевого резервирования. Эти сведения следует использовать в качестве отправной точки анализа. Например возможно, вы используете уровень обслуживания Standard hello с уровнем производительности S2. Hello среднее использование процентов для ЦП и ввода-вывода чтения и записи являются менее 40 процентов hello среднее число рабочих ролей меньше 50 и hello среднее число сеансов меньше 200. Рабочая нагрузка может поместиться в hello уровень производительности S1. Это легко toosee ли базы данных помещается в рабочей роли hello и предельных параметров сеанса. toosee ли базы данных помещается в более низкий уровень производительности с считает tooCPU, операции чтения и записи, разделите количество DTU hello hello низкий уровень производительности hello число DTU текущего уровня производительности и умножьте результат hello 100:
   
    **DTU S1 / DTU S2 * 100 = 20 / 50 * 100 = 40**
   
    результат Hello — hello относительная разница производительности между hello два уровня производительности в процентах. Если использование ресурсов не превышает это значение, рабочая нагрузка может поместиться в hello низкий уровень производительности. Тем не менее требуется toolook во все диапазоны значений использования ресурсов и определить, в процентах, как часто рабочей нагрузки базы данных может поместиться в hello низкий уровень производительности. Hello следующий запрос отображает hello в соответствии процент на измерение ресурсов, на основе порогового значения hello 40 процентов, который мы вычисляется в данном примере:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Исходя из вашей базы данных уровень обслуживания (SLO), можно ли рабочей нагрузки попадают hello низкий уровень производительности. Если рабочая нагрузка базы данных SLO — 99,9% и hello предыдущий запрос возвращает значение больше 99,9% для всех трех измерений ресурсов, рабочая нагрузка скорее всего, попадают hello низкий уровень производительности.
   
    Просмотрев процент соответствия hello также предоставляет регулировать ли следует переместить уровня toomeet Далее выше производительности toohello вашей цели уровня Обслуживания. Например userdb1 показывает hello после использования ЦП для hello прошлую неделю:
   
   | Средняя нагрузка ЦП, % | Максимальная нагрузка ЦП, % |
   | --- | --- |
   | 24,5 |100,00 |
   
    Средняя загрузка ЦП Hello — примерно четверти hello ограничения уровня производительности hello, которые попадают в hello уровень производительности базы данных hello. Но hello максимальное значение показывает, что hello базы данных достигает предела hello hello уровня производительности. Требуется toomove toohello следующий уровень производительности? Определить, как много раз рабочая нагрузка достигает 100 процентов и сравнивают его рабочая нагрузка базы данных tooyour цели уровня Обслуживания.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Если этот запрос возвращает значение меньше 99,9% для любого hello трех измерений ресурсов, рекомендуется либо скользящего toohello следующий уровень производительности или использовать настройки приложения hello-нагрузки tooreduce методы в базе данных SQL hello.
4. В этом упражнении также учитывает будущих увеличение hello вашей предполагаемой рабочей нагрузки.

Эластичные пулы можно выполнять мониторинг отдельных баз данных в пуле hello с hello методик, описанных в этом разделе. Однако вы можете отслеживать пул hello в целом. Дополнительные сведения см. в статье [Мониторинг пула эластичных баз данных и управление им на портале Azure](sql-database-elastic-pool-manage-portal.md).


### <a name="maximum-concurrent-requests"></a>Максимальное количество параллельных запросов
toosee hello число одновременных запросов, выполните этот запрос Transact-SQL в базе данных SQL.

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

Рабочая нагрузка hello tooanalyze локальной базы данных SQL Server и изменить toofilter этот запрос на hello конкретной базы данных будет tooanalyze. Например при наличии локальной базы данных, моябазаданных этот запрос Transact-SQL возвращает hello число одновременных запросов в этой базе данных:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Это только моментальный снимок в один момент времени. tooget лучше понять рабочей нагрузкой и требованиями одновременных запросов, вам потребуется toocollect большое количество примеров по времени.

### <a name="maximum-concurrent-logins"></a>Максимальное число параллельных операций входа
Можно анализировать вашего пользователя и приложения шаблоны tooget представление о частоты приветствия имен входа. Также можно запустить реальных загрузок в toomake для среды тестирования, убедиться, что вы не встретились это или других ограничений, которые мы обсудим в этой статье. Нет единого запроса или динамического административного представления, с помощью которых можно просмотреть количество параллельных операций входа или журнал.

Если несколько клиентов используют hello одинаковые строки подключения, hello служба проверяет подлинность каждого имени входа. Если 10 пользователей, одновременно подключаться hello tooa базы данных с помощью того же имени пользователя и пароля, будет 10 параллельных операций входа. Это ограничение применяется только toohello длительность hello входа и проверки подлинности. Если же 10 hello пользователи подключаются toohello базы данных последовательно, hello количество одновременных входов никогда не будет больше, чем 1.

> [!NOTE]
> В настоящее время это ограничение не применяется toodatabases в пулах эластичных БД.
> 
> 

### <a name="maximum-sessions"></a>Максимальное число сеансов
toosee hello число текущих активных сеансов, выполните этот запрос Transact-SQL в базе данных SQL.

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

При выполнении анализа рабочей нагрузки в локальной среде SQL Server, измените toofocus запроса hello конкретной базы данных. Этот запрос позволяет определить потребности возможных сеанс для базы данных hello, в противном случае его перемещения tooAzure базы данных SQL.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Опять же, эти запросы возвращают значение счетчика на определенный момент времени. Если со временем собрать несколько образцов, вы получите hello лучшее понимание сеанс использовать.

Для анализа базы данных SQL, можно получить исторические статистики на сеансах, запрашивая hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) представление и просмотрев hello **active_session_count** столбца. 
