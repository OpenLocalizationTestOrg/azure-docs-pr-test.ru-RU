---
title: "aaaBest и рекомендации для хранилища данных SQL Azure | Документы Microsoft"
description: "Рекомендации, которые следует учитывать при разработке решений для хранилища данных SQL Azure. Они помогут вам обеспечить эффективную работу."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Рекомендации по использованию хранилища данных SQL Azure
В этой статье — это совокупность многие рекомендации, которые помогут вам tooachieve оптимальной производительности в хранилище данных SQL Azure.  Некоторые основные понятия hello в этой статье, базовый и легко tooexplain, другие понятия и другие дополнительные, и мы просто scratch hello поверхности в этой статье.  Hello цель этой статьи — toogive некоторые основные рекомендации и tooraise осведомленность о toofocus важных областях, как вы построении хранилища данных.  Каждый раздел содержит описание tooa концепции, а затем выберите команду, что toomore подробные статьи, посвященные какие концепции hello титульных более подробно.

Если вы еще мало знакомы с хранилищем данных SQL Azure, некоторые разделы могут показаться вам очень сложными.  последовательность Hello разделы hello является главным образом в порядке важности hello.  При запуске сосредоточиться на hello несколько понятий, вы будете исправно.  Набравшись опыта работы с хранилищем данных SQL, вы можете приступить к изучению следующих понятий.  Будет выполнено длинные для всего toomake смысле.

## <a name="reduce-cost-with-pause-and-scale"></a>Снижение расходов за счет приостановки и масштабирования ресурсов
Это ключевой компонент хранилища данных SQL при возможности toopause hello не используются, который приостанавливает выставление счетов hello вычислительных ресурсов.  Другой ключевой особенностью является hello возможность tooscale ресурсов.  Приостановка и масштабирование можно сделать через портал Azure hello или с помощью команд PowerShell.  Ознакомиться с этими функциями как они может значительно снизить стоимость hello хранилищем данных, если она не используется.  Если всегда требуется хранилище данных доступен, можно tooconsider масштабов toohello наименьшего размера, DW100 вместо приостановки.

Ознакомьтесь с дополнительными сведениями о [приостановке][Pause compute resources] и [возобновлении][Resume compute resources] использования вычислительных ресурсов, а также об их [масштабировании].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Очистка транзакций перед приостановкой использования и масштабированием вычислительных ресурсов
При приостановке или масштабировать хранилище данных SQL фоновом hello запросы будут отменены при запуске hello приостановить или масштабировать запроса.  Отмена простой запрос SELECT операция выполняется очень быстро и почти не указано влияние toohello время, затрачиваемое toopause или масштабирование экземпляра.  Однако транзакций запросы, которые изменить структуру данных или hello hello данных, может оказаться toostop может быстро.  **Транзакционные запросы по определению должны полностью завершиться или выполнить откат изменений.**  Откат hello, выполненный запрос транзакций может занять как долго или даже больше, чем исходного изменения hello hello запрос применения.  Например если отменить запрос, который удаления строк и уже выполнения в течение часа, может потребоваться системы hello строк назад hello tooinsert час, которые были удалены.  При запуске, приостановить или масштабирования во время операции выполняются в полете вашей приостановить или масштабирование может показаться tootake длительное время, так как Приостановка и масштабирование имеет toowait для отката toocomplete hello для продолжения.

Дополнительные сведения см. в статьях [Транзакции в хранилище данных SQL][Understanding transactions] и [Оптимизация транзакций для хранилища данных SQL][Optimizing transactions].

## <a name="maintain-statistics"></a>Обеспечение статистики
В отличие от SQL Server, который автоматически обнаруживает и создает или обновляет статистику в столбцах, в хранилище данных SQL этот процесс необходимо выполнять самостоятельно.  Хотя мы планируем toochange оптимизированы в hello в будущем, для теперь требуется toomaintain вашей tooensure статистики, hello планы в хранилище данных SQL.  Hello планов, созданных оптимизатором hello доступны только в показанной hello доступной статистики.  **Создание выборочную статистику для каждого столбца tooget легко запускается со статистикой.**  Это одинаково важным tooupdate статистики также существенные изменения произойти tooyour данных.  Высокий уровень безопасности может быть tooupdate статистике ежедневно или после каждого нагрузки.  Всегда есть компромиссы между производительностью и стоимость hello toocreate и обновите статистику. Если обнаружится, что это занимает слишком много времени toomaintain все статистики, может понадобиться tootry toobe более селективным о есть статистика, какие столбцы или столбцы, которые необходимо частое обновление.  Например может потребоваться tooupdate столбцов даты, где новые значения могут быть добавлены, ежедневно. **Hello будет получить максимальную выгоду, наличие статистики для столбцов, участвующих в соединениях, столбцов, используемых в hello обнаружено предложение и столбцы в GROUP BY.**

Дополнительные сведения см. в статьях [Управление статистикой таблиц в хранилище данных SQL][Manage table statistics], [CREATE STATISTICS (Transact-SQL)][CREATE STATISTICS] и [UPDATE STATISTICS (Transact-SQL)][UPDATE STATISTICS].

## <a name="group-insert-statements-into-batches"></a>Объединение инструкций INSERT в группы
Небольшая таблица tooa одноразовый нагрузки с помощью инструкции INSERT или даже периодически перезагружает подстановки может работать нормально вашим потребностям, с помощью оператора, например `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Тем не менее если вам требуется tooload тысяч или миллионов строк в hello дня, может оказаться, что одноэлементный ВСТАВОК просто не справляются.  Вместо этого разработайте процессы, чтобы они записывают файл tooa и другой процесс, периодически поставляется и загружает этот файл.

Дополнительные сведения см. в статье [Инструкция INSERT (Transact-SQL)][INSERT].

## <a name="use-polybase-tooload-and-export-data-quickly"></a>Быстро использовать PolyBase tooload и экспорт данных
Хранилище данных SQL поддерживает загрузку и экспорт данных при помощи нескольких инструментов, включая фабрику данных Azure, PolyBase и BCP.  При работе с данными небольшого объема, что не требует высокой производительности, можно использовать любой инструмент.  Однако при загрузке или экспорт больших объемов данных, или требуется высокая производительность, PolyBase является наилучшим вариантом hello.  PolyBase — спроектированный tooleverage hello MPP (расширенной параллельной обработки) архитектура хранилища данных SQL таким образом загрузки и экспорт данных величины быстрее, чем любой другой инструмент.  Загрузку данных с помощью PolyBase можно выполнить, используя команды CTAS или INSERT INTO.  **С помощью CTAS позволит свести к минимуму ведение журнала транзакций и быстрым способом tooload hello данных.**  Фабрика данных Azure также поддерживает загрузку данных с помощью PolyBase.  PolyBase поддерживает различные форматы файлов, включая формат GZIP.  **toomaximize пропускная способность, при использовании gzip текстовые файлы, разрыв в 60 или более файлов toomaximize степенью параллелизма нагрузки.**  Кроме того, для повышения общей пропускной способности можно загружать данные одновременно.

Дополнительные сведения см. в статьях [Загрузка данных в хранилище данных Azure SQL][Load data], [Руководство по использованию PolyBase в хранилище данных SQL][Guide for using PolyBase], [Azure SQL Data Warehouse loading patterns and strategies][Azure SQL Data Warehouse loading patterns and strategies] (Стратегии и шаблоны загрузки данных в хранилище данных SQL Azure), [Загрузка данных в хранилище данных SQL с помощью фабрики данных][Load Data with Azure Data Factory], [Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure][Move data with Azure Data Factory], [Создание формата внешнего файла (Transact-SQL)][CREATE EXTERNAL FILE FORMAT] и [Функция Create Table As Select (CTAS) в хранилище данных SQL][Create table as select (CTAS)].

## <a name="load-then-query-external-tables"></a>Загрузка внешних таблиц и отправка запросов к ним
Polybase, также известные как внешние таблицы могут быть hello самый быстрый способ tooload данных, он не является оптимальным для запросов. В настоящее время таблицы Polybase хранилища данных SQL поддерживают только файлы больших двоичных объектов Azure. Эти файлы не обслуживаются какими-либо вычислительными ресурсами.  В результате хранилище данных SQL не переложить эту работу и таким образом необходимо прочитать весь файл hello, загрузив его tootempdb в данные о заказах tooread hello.  Таким образом Если имеется несколько запросов, которые будет выполнять запросы к данным, лучше tooload эти данные один раз и использовать локальную таблицу hello запросами.

Ознакомьтесь также с [руководством по использованию PolyBase][Guide for using PolyBase].

## <a name="hash-distribute-large-tables"></a>Хэш-распределение больших таблиц
По умолчанию таблицы распределяются по методу циклического перебора.  Это упрощает tooget пользователей к работе по созданию таблицы без необходимости toodecide распределение соответствующих таблиц.  Таблицы с распределением по методу циклического перебора могут вполне годиться для некоторых рабочих нагрузок, но в большинстве случаев намного эффективнее использовать столбец распределения.  При Hello наиболее распространенным примером при распределенных по столбцу таблицы значительно превосходят циклического таблицы соединяются две большие таблицы фактов.  Например при наличии таблицу orders, который распространяется по order_id и таблицу транзакций, которая также распространяется по order_id, при соединении таблицы транзакций tooyour таблицы заказов на order_id, этот запрос становится запроса к серверу, что означает Мы исключить операций перемещения данных.  Чем меньше в запросе действий, тем быстрее он выполняется.  Скорость выполнения запроса также зависит от объема перемещаемых данных.  Пояснения излагаются лишь основы hello поверхности. При загрузке распределенные таблицы, убедитесь, что входящие данные не сортируются по ключ распределения hello как замедлится вашей загружает.  См. ниже hello связывает за многие дополнительные сведения о как при выборе столбца распространения может повысить производительность, а также toodefine распределенные таблицы в предложении WITH hello инструкции СОЗДАНИЯ таблицы.

Дополнительные сведения см. в статьях [Общие сведения о таблицах в хранилище данных SQL][Table overview], [Распределение таблиц в хранилище данных SQL][Table distribution], [Создание таблицы (хранилище данных Azure SQL)][CREATE TABLE] и [Создание TABLE AS SELECT (хранилище данных Azure SQL)][CREATE TABLE AS SELECT], а также в статье, посвященной [выбору распределения таблицы][Selecting table distribution].

## <a name="do-not-over-partition"></a>Недопущение избыточного секционирования
Не смотря на то, что секционирование данных — это эффективный способ управления данными, который реализуется благодаря переключению секций или оптимизации сканирования путем исключения секций, наличие большого количества секций может повлиять на производительность запросов.  Стратегия разделения данных на большое количество секций, как правило, эффективна в SQL Server, но она не всегда работает в хранилище данных SQL.  Наличие слишком большого числа секций hello эффективность кластеризованные индексы columnstore также можно уменьшить, если каждая секция имеет не более 1 миллиона строк.  Следует помнить, что фоне hello, хранилище данных SQL разделяет данные для вас в 60 базы данных, поэтому при создании таблицы на 100 секций, это фактически приводит к 6000 секций.  Каждой рабочей нагрузки отличается, поэтому hello рекомендациям tooexperiment с секционированием toosee, что лучше всего работает для рабочей нагрузки.  В хранилище данных SQL можно использовать меньшее количество секций, чем в SQL Server.  Например, попробуйте использовать еженедельные или ежемесячные секции вместо ежедневных.

Дополнительные сведения см. в статье [Секционирование таблиц в хранилище данных SQL][Table partitioning].

## <a name="minimize-transaction-sizes"></a>Уменьшение размера транзакций
Инструкции INSERT, UPDATE и DELETE выполняются в транзакциях. В случае сбоя их необходимо откатить.  hello toominimize потенциальных long отката свести к минимуму размерами транзакций, когда это возможно.  Это можно сделать, разделив инструкции INSERT, UPDATE и DELETE на части.  Например если инструкции INSERT, который можно ожидать tootake 1 час, возможно, разделите hello INSERT на 4 части, которые будут каждое выполнение в течение 15 минут.  Использовать особых случаев минимального протоколирования, подобно CTAS, TRUNCATE, DROP TABLE или вставка tooempty таблиц tooreduce риск отката.  Другой способ tooeliminate откатов — toouse только метаданных операции, такие как переключение секций для управления данными.  Например, вместо этого, чем выполнение инструкции DELETE toodelete все строки в таблице, где был hello order_date в октябре 2001 г, можно секционировать данные ежемесячно и затем отключим hello секция с данными для пустую секцию из другой таблицы (см. ALTER Примеры ТАБЛИЦ).  Для несекционированной таблицы можно с помощью данных hello toowrite CTAS, требуется tookeep в таблице, а не на использование инструкции DELETE.  Если CTAS принимает Здравствуйте одинаковое количество времени, это будет гораздо более безопасной toorun операции, поскольку оно ведение журнала транзакций с минимальными и может быть отменено быстро, при необходимости.

Дополнительные сведения см. в статьях [Транзакции в хранилище данных SQL][Understanding transactions], [Оптимизация транзакций для хранилища данных SQL][Optimizing transactions], [Секционирование таблиц в хранилище данных SQL][Table partitioning], а также в статьях об инструкциях [TRUNCATE TABLE][TRUNCATE TABLE] и [ALTER TABLE][ALTER TABLE] и статье [Функция Create Table As Select (CTAS) в хранилище данных SQL][Create table as select (CTAS)].

## <a name="use-hello-smallest-possible-column-size"></a>Используйте hello наименьший размер столбцов
При определении DDL, с использованием типа данных наименьшего hello, поддерживающий данных улучшит производительность запросов.  Это особенно важно для столбцов CHAR и VARCHAR.  Если hello длинного значения в столбце 25 символов, затем определите столбца как VARCHAR(25).  Не рекомендуется определять все столбцы tooa больших по умолчанию символов.  Кроме того, по возможности определяйте столбцы как VARCHAR, а не NVARCHAR.

Дополнительные сведения см. в статьях, посвященных [общим сведениям о таблицах][Table overview], [типам данных таблиц][Table data types] и [инструкции CREATE TABLE][CREATE TABLE].

## <a name="use-temporary-heap-tables-for-transient-data"></a>Использование временных таблиц без кластеризованных индексов для хранения временных данных
При временно размещения данных в хранилище данных SQL, может обнаружиться, что использование кучи таблицы сделает быстрее hello общий процесс.  При загрузке данных только toostage его перед выполнением дополнительные преобразования, загрузка tooheap hello таблица будет намного быстрее, чем загрузка данных tooa hello кластеризованный columnstore таблицы.  Кроме того загрузка данных tooa временной таблицы также будут загружаться гораздо быстрее, чем загрузка хранилища toopermanent таблицы.  Временные таблицы начинаться с «#» и доступны только в сеансе hello, создавшей его, поэтому они могут работать только в ограниченных сценариях.   Таблицы в куче, определяются в предложение WITH hello CREATE TABLE.  При использовании временной таблицы слишком помните toocreate статистические данные для этой временной таблицы.

Дополнительные сведения см. в статьях о [временных таблицах][Temporary tables], [инструкциях CREATE TABLE][CREATE TABLE] и [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT].

## <a name="optimize-clustered-columnstore-tables"></a>Оптимизация таблиц с кластеризованными индексами columnstore
Кластеризованные индексы columnstore являются одним из наиболее эффективных способов hello, данные можно хранить в хранилище данных SQL Azure.  По умолчанию в хранилище данных SQL используются таблицы с кластеризованными индексами Columnstore.  Важно tooget hello максимальную производительность запросов в таблицах columnstore, в которых сегмент хорошее качество.  При строки записываются toocolumnstore таблиц в условиях нехватки памяти, качество сегмента columnstore может упасть.  Качество сегмента можно изменить по числу строк в сжатой группе строк.  . В разделе hello [причины низкой columnstore индекса качества] [ Causes of poor columnstore index quality] в hello [таблицы индексов] [ Table indexes] статью пошаговые инструкции по обнаружение и повышение качества сегмента для таблицы в кластеризованный индекс columnstore.  Поскольку сегментов columnstore высокого качества является важной, это рекомендуется toouse идентификаторы пользователей, находящихся в класс hello среднего или крупного ресурса для загрузки данных.  Здравствуйте, меньше Dwu используется, hello большего hello ресурсов класса, вы будете tooyour tooassign загрузке пользователя.

Поскольку таблиц columnstore обычно не Принудительная отправка данных в сжатые columnstore сегмент до более 1 миллиона строк одной таблицы и каждого хранилища данных SQL таблица секционирована на 60 таблиц, как правило, таблицы columnstore не получается выигрыш запроса Если таблица hello имеет более 60 миллиона строк.  Для таблицы с менее 60 миллионов строк может быть любой toohave смысле индекс columnstore.  Для таблицы с количеством строк менее 60 миллионов бессмысленно использовать индекс Columnstore, хотя он и не повлияет на производительность.  Кроме того Если выполнено секционирование данных, затем требуется tooconsider необходимость toobenefit toohave 1 миллион строк из кластеризованного индекса columnstore каждой секции.  Если таблица имеет 100 секций, то он должен быть по крайней мере один миллиард 6 toohave toobenefit строк из хранилища кластеризованных столбцов (60 распределения * 100 секций * 1 миллион строк).  Если таблица не имеет 6 миллиарда строк в этом примере, сократите число hello секций или попробуйте вместо таблицы кучи.  Также возможно, стоит экспериментируете toosee Если повышения производительности могут быть получены с помощью таблицы кучи с вторичных индексов, а не в таблицу columnstore.  Таблицы ColumnStore еще не поддерживают вторичные индексы.

При запросе таблицы columnstore, запросы будут выполняться быстрее, если выбрать только необходимые столбцы hello.  

Ознакомьтесь также со статьями [Индексирование таблиц в хранилище данных SQL][Table indexes], [Руководство по индексам columnstore][Columnstore indexes guide] и разделом с [описанием повторной сборки индексов columnstore][Rebuilding columnstore indexes].

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Используйте увеличить производительность запросов tooimprove класса ресурсов
Хранилище данных SQL использует группы ресурсов в качестве tooqueries памяти tooallocate способом.  В стандартной hello все пользователи назначаются toohello мало ресурсов класса, который предоставляет 100 МБ памяти для каждого распространителя.  Поскольку всегда существует 60 распределения и каждого распределения предоставляется менее 100 МБ, расширенный hello областей памяти выделения — 6 000 МБ или в 6 ГБ.  Некоторые запросы, как большой соединения или таблиц columnstore tooclustered загрузок, будет обеспечен больше операций выделения памяти.  На выполнение некоторых запросов, таких как запросы на обычное сканирование, память не требуется.  На hello другой стороны использование классов больше ресурсов влияет параллелизм, поэтому рекомендуется tootake это во внимание перед перемещением все пользователи tooa больших ресурсов класса.

Дополнительные сведения см. в статье [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Concurrency and workload management].

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Используйте меньше ресурсов класса tooIncrease параллелизма
Если отметить, что пользователь запросов показаться toohave длительная задержка, возможно, пользователи работают в классах больше ресурсов и потребляют много слоты параллелизма, вызывая другие запросы tooqueue вверх.  toosee, если запросы пользователей находятся в очереди, запустите `SELECT * FROM sys.dm_pdw_waits` toosee, если возвращаются все строки.

Дополнительные сведения см. в статьях [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Concurrency and workload management] и [sys.dm_pdw_waits (Transact-SQL)][sys.dm_pdw_waits].

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Используйте динамические административные представления toomonitor и оптимизации запросов
Хранилище данных SQL имеет несколько динамических административных представлений, которые могут быть используется toomonitor выполнения запроса.  Hello мониторинга статье рассматриваются пошаговые инструкции на как toolook подробностей hello выполняющегося запроса.  tooquickly запросов поиска в эти динамические административные представления, с помощью параметра LABEL hello с запросами может помочь.

Дополнительные сведения см. в статьях [Мониторинг рабочей нагрузки с помощью динамических административных представлений][Monitor your workload using DMVs], [Использование меток для инструментирования запросов в хранилище данных SQL][LABEL], [Предложение OPTION (Transact-SQL)][OPTION], [sys.dm_exec_sessions (Transact-SQL)][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests (Transact-SQL)][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_request_steps (Transact-SQL)][sys.dm_pdw_sql_requests], [ys.dm_pdw_dms_workers (Transact-SQL)], [DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)][DBCC PDW_SHOWEXECUTIONPLAN] и [sys.dm_pdw_waits (Transact-SQL)][sys.dm_pdw_waits].

## <a name="other-resources"></a>Другие ресурсы:
Дополнительные сведения о распространенных проблемах и способах их решения см. в статье [Устранение неполадок хранилища данных SQL Azure][Troubleshooting].

Если вы не нашли то, что вы искали, в этой статье, попробуйте использовать hello «Поиск для документы» hello левой части этой страницы toosearch всех документов hello хранилище данных SQL Azure.  Hello [форум MSDN хранилища данных SQL Azure] [ Azure SQL Data Warehouse MSDN Forum] было создать как место для вас tooask вопросы пользователей tooother и toohello группы продукта хранилища данных SQL.  Мы активно отслеживать этот форум tooensure, что свои вопросы ответы на или по другим пользователем или один из нас.  При желании tooask свои вопросы о переполнении стека в нам требуется также [Azure хранилища стека переполнения форум по данным SQL][Azure SQL Data Warehouse Stack Overflow Forum].

Наконец, используйте hello [отзывов о хранилище данных SQL Azure] [ Azure SQL Data Warehouse Feedback] toomake функции запросов к страницам.  Ваши отзывы и голоса за отзывы, оставленные другими пользователями, помогут нам определить, какие улучшения функций наиболее приоритетные.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[масштабировании]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[ys.dm_pdw_dms_workers (Transact-SQL)]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
