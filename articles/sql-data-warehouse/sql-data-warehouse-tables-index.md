---
title: "Индексирование таблиц в хранилище данных SQL | Microsoft Azure"
description: "Начало работы с индексированием таблиц в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jenniehubbard
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 12/06/2017
ms.author: barbkess
ms.openlocfilehash: 672270536a7405e617edbcf5ec0e6eff68be7fde
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Индексирование таблиц в хранилище данных SQL
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Типы данных][Data Types]
> * [Распределение][Distribute]
> * [Индекс][Index]
> * [Секция][Partition]
> * [Статистика][Statistics]
> * [Временные таблицы][Temporary]
> 
> 

В хранилище данных SQL предоставляется несколько вариантов индексирования, включая использование [кластеризованных индексов Columnstore][clustered columnstore indexes], а также [кластеризованных и некластеризованных индексов][clustered indexes and nonclustered indexes].  Кроме того, также предоставляется вариант без использования индексов — использование [кучи][heap].  В этой статье рассматриваются преимущества каждого типа индексирования, а также приведены способы достижения максимальной производительности при использовании индексов. Дополнительные сведения о создании таблиц в хранилище данных SQL см. в статье [СОЗДАНИЕ ТАБЛИЦЫ (хранилище данных Azure SQL)][create table syntax].

## <a name="clustered-columnstore-indexes"></a>Кластеризованные индексы Columnstore
Если для таблицы не заданы параметры индексирования, по умолчанию хранилище данных SQL создает кластеризованный индекс Columnstore. Кластеризованные таблицы Columnstore обеспечивают максимальную производительность запросов, а также самый высокий уровень сжатия данных.  Обычно эти таблицы более эффективны, чем таблицы с кластеризованными индексами и таблицы без кластеризованных индексов, и их рекомендуется использовать в больших таблицах.  Таким образом, если вы не уверены, какой метод индексации применить к вашей таблице, используйте кластеризованные индексы Columnstore.  

Чтобы создать таблицу с кластеризованным индексом Columnstore, опустите предложение WITH или укажите в нем параметр CLUSTERED COLUMNSTORE INDEX.

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Есть несколько сценариев, в которых не рекомендуется использовать кластеризованный индекс Columnstore.

* Таблицы Columnstore не поддерживают типы данных VARCHAR(MAX), NVARCHAR(MAX) и VARBINARY(MAX).  В этом случае рекомендуется использовать кучу или кластеризованный индекс.
* Таблицы Columnstore менее эффективны для хранения временных данных.  В этом случае рекомендуется использовать таблицы без кластеризованных индексов и, возможно, даже временные таблицы.
* При наличии небольших таблиц, содержащих меньше 100 млн строк.  В этом случае рекомендуется использовать таблицы без кластеризованных индексов.

## <a name="heap-tables"></a>Таблицы без кластеризованных индексов
Если вам необходимо временно разместить данные в хранилище данных SQL, использование таблицы без кластеризованных индексов может существенно сократить время загрузки данных.  Это связано с тем, что загрузка в кучи выполняется быстрее, чем в таблицы с кластеризованными индексами, и в некоторых случаях из кэша можно выполнять последующее считывание.  Загрузка таблицы в таблицу без кластеризованных индексов перед выполнением преобразования данных выполняется намного быстрее, чем загрузка данных в таблицу с кластеризованными индексами Columnstore. Кроме того, загрузка данных во [временную таблицу][Temporary] выполняется гораздо быстрее, чем загрузка таблицы в постоянное хранилище.  

Для небольших таблиц подстановки (менее 100 миллионов строк) рекомендуется использовать таблицы без кластеризованных индексов.  Сжатие в кластеризованных таблицах Columnstore выполнятся оптимально при наличии более 100 миллионов строк.

Чтобы создать таблицу без кластеризованных индексов, укажите в предложении WITH параметр HEAP.

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Кластеризованные и некластеризованные индексы
Кластеризованные индексы могут быть более эффективны, когда требуется извлечь отдельную строку.  Кластеризованные или вторичные некластеризованные индексы рекомендуется использовать, если требуется выполнить запросы на очень быструю подстановку одной или нескольких строк в таблицу.  Недостаток использования кластеризованного индекса заключается в том, что эффективными будут только те запросы, в которых используется высокоизбирательный фильтр для столбца с кластеризованным индексом.  Чтобы улучшить фильтр в других столбцах, добавьте в них некластеризованный индекс.  Однако каждый добавленный в таблицу индекс увеличивает пространство и время обработки загрузки.

Чтобы создать таблицу с кластеризованным индексом, укажите в предложении WITH параметр CLUSTERED INDEX.

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

Чтобы добавить некластеризованный индекс для таблицы, просто используйте приведенный ниже синтаксис.

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Оптимизация кластеризованных индексов Columnstore
В кластеризованных таблицах Columnstore данные упорядочены по сегментам.  Качество сегментов существенно влияет на эффективность выполнения запросов в таблице Columnstore.  Его можно определить по числу строк в сжатой группе строк.  Наиболее оптимальное качество сегментов достигается в таблицах, где на сжатую группу строк приходится по крайней мере 100 тысяч строк, а производительность увеличивается при достижении максимального количества строк на группу — 1 048 576.

Для вычисления среднего количества строк для каждой группы строк и определения неоптимальных кластеризованных индексов Columnstore можно создать и использовать представление, подобное приведенному ниже.  Последний столбец в этом представлении создаст инструкцию SQL, которую можно использовать для перестроения индексов.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

После создания представления выполните этот запрос, чтобы определить таблицы с группами строк, содержащими менее 100 тысяч строк.  Если требуется достичь более оптимального качества сегментов, пороговое значение числа строк можно увеличить. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

После выполнения запроса можно начать просмотр данных и анализ результатов. В таблице ниже показано, на какие данные следует обратить внимание при анализе групп строк.

| столбец | Как использовать эти данные |
| --- | --- |
| [table_partition_count] |Если таблица секционирована, то счетчики открытых групп строк могут быть больше. Каждая секция в распределении теоретически может иметь связанную с ней открытую группу строк. Это следует учитывать при анализе. Небольшую секционированную таблицу можно оптимизировать, полностью отменив секционирование, так как это улучшит сжатие. |
| [row_count_total] |Общее количество строк в таблице. Например, это значение можно использовать для вычисления процента строк в сжатом состоянии. |
| [row_count_per_distribution_MAX] |Если все строки распределены равномерно, это значение будет целевым числом строк для каждого распределения. Сравните это значение с compressed_rowgroup_count. |
| [COMPRESSED_rowgroup_rows] |Общее количество строк в формате columnstore для таблицы. |
| [COMPRESSED_rowgroup_rows_AVG] |Если среднее количество строк существенно меньше максимального числа строк для группы строк, возможно, стоит использовать инструкции CTAS или ALTER INDEX REBUILD для повторного сжатия данных. |
| [COMPRESSED_rowgroup_count] |Число групп строк в формате columnstore. Очень большое относительно таблицы число указывает на то, что плотность columnstore низка. |
| [COMPRESSED_rowgroup_rows_DELETED] |Логически удаленные строки в формате columnstore. Если это число велико относительно размера таблицы, возможно, стоит создать секцию заново или перестроить индекс, так как в этом случае они удаляются физически. |
| [COMPRESSED_rowgroup_rows_MIN] |Используйте это значение вместе со столбцами AVG и MAX, чтобы оценить диапазон размеров для групп строк в индексе Columnstore. Небольшое значение относительно порогового значения загрузки (102 400 для распределения с выравниванием по секциям) говорит о том, что загрузку данных можно оптимизировать. |
| [COMPRESSED_rowgroup_rows_MAX] |То же, что и выше |
| [OPEN_rowgroup_count] |Открытые группы строк допускаются. Ожидается наличие одной открытой группы строк на каждое распределение таблиц (60). Очень большие числа говорят о загрузке данных в разные секции. Внимательно проверьте стратегию секционирования, чтобы убедиться в ее эффективности |
| [OPEN_rowgroup_rows] |Каждая группа строк может иметь максимум 1 048 576 строк. Используйте это значение для оценки текущей наполненности открытых групп строк. |
| [OPEN_rowgroup_rows_MIN] |Наличие открытых групп указывает, что либо данные медленно загружаются в таблицу, либо предыдущая загрузка привела к переносу оставшихся строк в эту группу строк. С помощью столбцов MIN, MAX, AVG можно узнать, сколько данных находится в открытых группах строк. Для небольших таблиц это может быть 100 % всех данных! В этом случае следует использовать инструкцию ALTER INDEX REBUILD, чтобы принудительно перенести данные в columnstore. |
| [OPEN_rowgroup_rows_MAX] |То же, что и выше |
| [OPEN_rowgroup_rows_AVG] |То же, что и выше |
| [CLOSED_rowgroup_rows] |Для проверки оцените число строк в закрытых группах строк. |
| [CLOSED_rowgroup_count] |Число закрытых групп строк должно быть небольшим (если они вообще присутствуют). Закрытые группы строк можно преобразовать в сжатые группы строк с помощью инструкции ALTER INDEX. REORGANISE. Однако обычно это не требуется. Закрытые группы автоматически преобразуются в группы строк Columnstore фоновым процессом "переноса кортежей". |
| [CLOSED_rowgroup_rows_MIN] |Закрытые группы строк должны иметь очень высокий коэффициент заполнения. Если коэффициент заполнения для закрытой группы строк низок, то требуется дальнейший анализ Columnstore. |
| [CLOSED_rowgroup_rows_MAX] |То же, что и выше |
| [CLOSED_rowgroup_rows_AVG] |То же, что и выше |
| [Rebuild_Index_SQL] |Инструкция SQL, которая используется для перестроения индекса Columnstore таблицы. |

## <a name="causes-of-poor-columnstore-index-quality"></a>Причины низкого качества индекса Columnstore
Если вы обнаружили таблицы с сегментами низкого качества, необходимо определить причину.  Ниже описаны распространенные причины низкого качества сегментов:

1. Нехватка памяти при создании индекса.
2. Высокая интенсивность операций DML.
3. Небольшой объем операций загрузки или потоковые загрузки
4. Слишком много секций

По приведенным выше причинам количество строк в каждой группе будет значительно меньше 1 миллиона.  Кроме того, вместо перехода в сжатую группу строки могут попасть в разностную группу строк. 

### <a name="memory-pressure-when-index-was-built"></a>Нехватка памяти при создании индекса.
Количество строк в сжатой группе строк непосредственно зависит от ширины строк и объема памяти, доступного для обработки группы строк.  Если во время записи строк в таблицы Columnstore возникает нехватка памяти, качество сегмента Columnstore может ухудшиться.  Поэтому для записи строк в таблицы Columnstore рекомендуется выделить максимально возможный объем памяти.  Так как показатели памяти и параллелизма взаимосвязаны, выделение памяти зависит от класса данных в каждой строке таблицы, числа единиц базы данных хранилища данных, выделенного для системы, а также числа слотов выдачи, доступного для записи данных в таблицу.  Рекомендации по минимальному классу ресурсов: xlargerc для DW300 или ниже, largerc для DW400–DW600 и mediumrc для DW1000 и выше.

### <a name="high-volume-of-dml-operations"></a>Высокая интенсивность операций DML.
Интенсивные операции DML по обновлению и удалению строк приводят к неэффективной работе Columnstore. Это особенно верно в случае изменения большей части строк в группе строк.

* Если строка удаляется из сжатой группы строк, она лишь логически помечается как удаленная. Строка остается в сжатой группе строк до перестроения секции или таблицы.
* При вставке строка добавляется во внутреннюю таблицу rowstore, называемую разностной группой строк. Вставленная строка не преобразуется в Columnstore до тех пор, пока разностная группа строк не будет заполнена и помечена как закрытая. Группы строк закрываются после достижения максимального объема в 1 048 576 строк. 
* Обновление строки в формате columnstore обрабатывается как логическое удаление, а затем — как вставка. Вставленную строку можно сохранить в разностном хранилище.

Пакетные операции обновления и вставки, превышающие пороговое значение в 102 400 строк для распределения с выравниванием по секциям, записываются непосредственно в формате columnstore. Чтобы это произошло, при условии равномерного распределения потребуется изменить более 6,144 млн строк в рамках одной операции. Если количество строк для распределения с выравниванием по секциям не превышает 102 400, строки будут отправляться в разностное хранилище и останутся там до тех пор, пока не будет вставлено или изменено количество строк, достаточное для закрытия группы строк, или не будет перестроен индекс.

### <a name="small-or-trickle-load-operations"></a>Небольшой объем операций загрузки или потоковые загрузки
Небольшие загрузки, поступающие в хранилище данных SQL, иногда называют потоковыми. Обычно они представляют собой практически постоянный поток данных, принимаемых системой. Однако поскольку этот поток является не совсем непрерывным, объем строк невелик. Чаще всего количество данных значительно ниже порогового значения, необходимого для непосредственной загрузки в формате columnstore.

В таких ситуациях рекомендуется сначала разместить данные в хранилище BLOB-объектов Azure, накопить их и лишь затем загрузить. Этот метод часто называют *микропакетной обработкой*.

### <a name="too-many-partitions"></a>Слишком много секций
На качество индекса также влияет секционирование в кластеризованных таблицах Columnstore.  Перед секционированием данные в хранилище данных SQL разбиваются на 60 баз данных.  Во время секционирования выполняется дальнейшее разделение данных.  Чтобы воспользоваться преимуществами кластеризованного индекса columnstore при секционировании данных, **каждая** секция должна содержать по крайней мере 1 миллион строк.  Если таблица состоит из 100 секций, то чтобы использовать кластеризованный индекс columnstore, она должна состоять как минимум из 6 миллиардов строк (60 распределений * 100 секций * 1 миллион строк). Если эта таблица не содержит такого количества строк, рекомендуется уменьшить количество секций или использовать таблицу без кластеризованных индексов.

Когда в таблицу будут загружены данные, чтобы определить и перестроить таблицы с неоптимальными кластеризованными индексами Columnstore, выполните приведенные ниже действия.

## <a name="rebuilding-indexes-to-improve-segment-quality"></a>Повышение качества сегментов за счет перестроения индексов
### <a name="step-1-identify-or-create-user-which-uses-the-right-resource-class"></a>Шаг 1. Определение или создание пользователя, который использует соответствующий класс ресурсов
Простой способ быстро повысить качество сегментов — перестроить индекс.  Инструкция SQL, возвращенная в предыдущем представлении, возвращает инструкцию ALTER INDEX REBUILD, которую можно использовать для перестроения индексов.  При перестроении индексов требуется, чтобы для сеанса был выделен достаточный объем памяти.  Для этого повысьте класс ресурсов для пользователя, который имеет разрешение на перестроение индекса для этой таблицы, до рекомендованного минимального класса ресурсов.  Класс ресурсов пользователя владельца базы данных нельзя изменить, поэтому если вы не создали пользователя в системе, вам потребуется сделать это.  Рекомендации по минимальному классу ресурсов: xlargerc для DW300 или ниже, largerc для DW400–DW600 и mediumrc для DW1000 и выше.

Ниже приведен пример того, как можно выделить дополнительный объем памяти для пользователя, увеличив класс ресурсов.  Дополнительные сведения о классах ресурсов и создании пользователя см. в статье [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Concurrency].

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Шаг 2. Перестройка кластеризованных индексов Columnstore, используя пользователя с более высоким классом ресурсов
Войдите в систему от имени пользователя из шага 1 (например, LoadUser), которому теперь соответствует более высокий класс ресурсов, и выполните инструкции ALTER INDEX.  Убедитесь, что этот пользователь имеет разрешение ALTER в отношении таблиц, в которых будет выполнятся перестроение индекса.  В этих примерах показано перестроение всего индекса Columnstore и перестроение одной секции. В больших таблицах целесообразно перестроить только одну секцию за раз.

Кроме того, вместо перестроения индекса можно копировать таблицу в новую таблицу, используя инструкцию [CTAS][CTAS].  Какой способ лучше? Для больших объемов данных инструкция [CTAS][CTAS] обычно выполняется быстрее, чем [ALTER INDEX][ALTER INDEX]. Что же касается небольших объемов данных, рекомендуется использовать инструкцию [ALTER INDEX][ALTER INDEX]. Она проще в использовании и не требует замены таблицы.  Дополнительные сведения о перестроении индексов с использованием инструкции CTAS см. в **этом разделе**.

```sql
-- Rebuild the entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

В хранилище данных SQL операция перестроения индекса выполняется в автономном режиме.  Дополнительные сведения о перестройке индексов см. в разделе об использовании инструкции ALTER INDEX REORGANIZE в руководствах по [дефрагментация индексов columnstore][Columnstore Indexes Defragmentation] и работе с [ALTER INDEX][ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Шаг 3. Проверка улучшения качества кластеризованных сегментов Columnstore
Повторно выполните запрос на определение таблицы с сегментами низкого качества и убедитесь, что качество сегментов улучшилось.  Если это не так, возможно, в таблице слишком широкие строки.  Если для перестроения индексов требуется более высокий объем памяти,

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Перестроение индексов с помощью инструкции CTAS и переключения секций
В этом примере для перестроения секции таблицы используется инструкция [CTAS][CTAS] и переключение секций. 

```sql
-- Step 1: Select the partition of data and write it out to a new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT the data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 TO  [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN the rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 TO  [dbo].[FactInternetSales] PARTITION 2;
```

Дополнительные сведения о перестроении секций с помощью `CTAS` см. в статье, посвященной [секционировании таблиц в хранилище данных SQL][Partition].

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в статьях, посвященных [общим сведениям о таблицах][Overview], [типам данных таблиц][Data Types], [распределению таблицы][Distribute], [секционированию таблицы][Partition], [управлению статистикой таблиц][Statistics] и [временным таблицам][Temporary].  Дополнительные сведения см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
