---
title: "aaaIndexing таблиц в хранилище данных SQL | Microsoft Azure"
description: "Начало работы с индексированием таблиц в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
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

В хранилище данных SQL предоставляется несколько вариантов индексирования, включая использование [кластеризованных индексов Columnstore][clustered columnstore indexes], а также [кластеризованных и некластеризованных индексов][clustered indexes and nonclustered indexes].  Кроме того, также предоставляется вариант без использования индексов — использование [кучи][heap].  В этой статье рассматриваются преимущества hello каждого типа индекса, а также советы toogetting hello большинство производительность из ваших индексов. В разделе [таблиц синтаксис инструкции create] [ create table syntax] для получения дополнительных сведений о том, как toocreate таблица в хранилище данных SQL.

## <a name="clustered-columnstore-indexes"></a>Кластеризованные индексы Columnstore
Если для таблицы не заданы параметры индексирования, по умолчанию хранилище данных SQL создает кластеризованный индекс Columnstore. Кластеризованный индекс columnstore таблицы обеспечивают обоих hello высокой степени сжатия данных, а также hello лучшую общую производительность.  Кластеризованный индекс columnstore таблицы обычно будет превосходят кластеризованные таблицы, индекса или кучи и обычно являются hello наилучшим образом подходят для больших таблиц.  По этим причинам кластеризованный индекс columnstore — наиболее toostart месте hello в нет уверенности в правильности tooindex таблицы.  

toocreate таблице кластеризованный индекс columnstore, просто укажите КЛАСТЕРИЗОВАННЫЙ индекс COLUMNSTORE в предложении WITH hello или не указывать предложение WITH hello:

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
При временно размещения данных в хранилище данных SQL, может обнаружиться, что использование кучи таблицы сделает быстрее hello общий процесс.  Это так, как работают быстрее, чем таблицы tooindex tooheaps загружает и в некоторых случаях hello последующих чтения может выполняться из кэша.  При загрузке данных только toostage его перед выполнением дополнительные преобразования, загрузка tooheap hello таблица будет намного быстрее, чем загрузка данных tooa hello кластеризованный columnstore таблицы. Кроме того, при загрузке данных tooa [временной таблицы] [ Temporary] также будет загружаться гораздо быстрее, чем загрузка хранилища toopermanent таблицы.  

Для небольших таблиц подстановки (менее 100 миллионов строк) рекомендуется использовать таблицы без кластеризованных индексов.  Кластер таблиц columnstore начать оптимального сжатия tooachieve после более чем 100 миллионов строк.

toocreate таблицы кучи, просто укажите КУЧИ в предложении WITH hello:

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
Кластеризованные индексы могут превосходят таблиц в кластеризованном необходимости toobe быстро получить одну строку.  Для запросов, где один или очень мало строки подстановки — необходимые tooperformance extreme скорость учитывайте кластерный индекс или вторичный некластеризованный индекс.  Недостаток Hello toousing кластеризованного индекса — что смогут воспользоваться только запросы, которые используют высокой избирательностью фильтра hello кластеризованный индекс столбца.  tooimprove фильтр на другие столбцы, которые некластеризованный индекс может быть добавлен tooother столбцов.  Однако каждый индекс, который добавляется в таблицу tooa будет добавлена и пространства tooloads времени обработки.

toocreate кластеризованного индекса таблицы, достаточно указать КЛАСТЕРИЗОВАННОГО ИНДЕКСА в предложении WITH hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd некластеризованный индекс в таблице, просто используйте hello, используя синтаксис:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Оптимизация кластеризованных индексов Columnstore
В кластеризованных таблицах Columnstore данные упорядочены по сегментам.  Наличие качества верхний сегмент является критических tooachieving оптимальной производительности запросов в таблицу columnstore.  Качество сегмент может измеряться hello количество строк в группе сжатая строка.  Сегмент качества оптимальный, где имеется по крайней мере 100 КБ строк в сжатых строку группы и получить производительности, как hello число строк на каждую строку группы подход 1 048 576 строк, равное hello большинство строк, которое может содержать группы строк.

можно создать и использовать Hello под представлением в вашей системе toocompute hello среднее строк на каждую строку, группировку и идентификацию все индексы columnstore неоптимальной кластера.  Hello последний столбец для этого представления создаст как инструкцию SQL, который можно использовать toorebuild индексов.

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

После создания представления hello выполните этот запрос tooidentify таблицы с группами строк с менее 100 тысяч строк.  Конечно может потребоваться tooincrease hello порогового значения 100 КБ, если вы ищете дополнительные сегмент оптимального качества. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

После выполнения запроса hello можно начать toolook данных hello и анализировать результаты. В следующей таблице показано, какие toolook для анализа группы строк.

| столбец | Как toouse эти данные |
| --- | --- |
| [table_partition_count] |Если hello таблица секционирована, может ожидать toosee выше строки, откройте группу счетчиков. Каждая секция в распределении hello в теории возможны открытая группа строк связанные с ним. Это следует учитывать при анализе. Небольшая таблица, разбитый на разделы можно оптимизировать, удалив hello секционирование полностью, как это позволяет улучшить сжатия. |
| [row_count_total] |Общее число строк для таблицы hello. Например можно использовать это значение toocalculate процент строк в состоянии hello сжимаются. |
| [row_count_per_distribution_MAX] |Если все строки равномерно распределяются hello целевое количество строк на распространения следует значение. Сравните это значение с hello compressed_rowgroup_count. |
| [COMPRESSED_rowgroup_rows] |Общее число строк в формате columnstore для таблицы hello. |
| [COMPRESSED_rowgroup_rows_AVG] |Если hello среднее число строк значительно меньше, чем hello максимальное число строк для группы строк, рассмотрите возможность использования CTAS или ALTER INDEX REBUILD toorecompress hello данных |
| [COMPRESSED_rowgroup_count] |Число групп строк в формате columnstore. Если это число очень высокого уровня в таблице toohello отношений это индикатора, плотность columnstore hello оказался низким. |
| [COMPRESSED_rowgroup_rows_DELETED] |Логически удаленные строки в формате columnstore. Если номер hello большой относительный размер tootable, рассмотрите возможность повторного создания секции hello или перестроения индекса hello, как при этом удаляется физически. |
| [COMPRESSED_rowgroup_rows_MIN] |Используйте в сочетании с hello и MAX, AVG столбцы toounderstand hello диапазон значений для группы строк hello в вашей columnstore. Небольшое значение выше порогового значения загрузки hello (102 400 каждого выровнены по секциям распространения) предлагает оптимизации доступны в hello загрузки данных |
| [COMPRESSED_rowgroup_rows_MAX] |То же, что и выше |
| [OPEN_rowgroup_count] |Открытые группы строк допускаются. Ожидается наличие одной открытой группы строк на каждое распределение таблиц (60). Очень большие числа говорят о загрузке данных в разные секции. Hello Проверьте правильность его звуковой toomake стратегии секционирования |
| [OPEN_rowgroup_rows] |Каждая группа строк может иметь максимум 1 048 576 строк. Используйте это значение toosee степень заполнения группы откройте строку hello, |
| [OPEN_rowgroup_rows_MIN] |Откройте "группы" Указывает, что данные тонкого загружаемых в таблицу hello или который hello предыдущей загрузки, сброшенных на оставшиеся строки в этой группе строк. Используйте hello MIN, MAX, AVG toosee столбцы, какой объем данных, находился в групп строк OPEN. Для небольших таблиц это может быть 100% от всех данных hello! В этом случае инструкция ALTER INDEX REBUILD tooforce hello toocolumnstore данных. |
| [OPEN_rowgroup_rows_MAX] |То же, что и выше |
| [OPEN_rowgroup_rows_AVG] |То же, что и выше |
| [CLOSED_rowgroup_rows] |Рассмотрим hello закрыт строка группы строк в качестве проверочной. |
| [CLOSED_rowgroup_count] |Hello количество закрытых групп строк должно быть низким, если все видимые вообще. Закрытых групп строк может быть преобразованный toocompressed rowg по с помощью hello ALTER INDEX... REORGANISE. Однако обычно это не требуется. Закрытые группы — группы строк автоматически преобразованный toocolumnstore процессом «кортежей» hello фона. |
| [CLOSED_rowgroup_rows_MIN] |Закрытые группы строк должны иметь очень высокий коэффициент заполнения. В случае низкой скорости заполнения hello для группы строк closed дальнейшего анализа hello columnstore является обязательным. |
| [CLOSED_rowgroup_rows_MAX] |То же, что и выше |
| [CLOSED_rowgroup_rows_AVG] |То же, что и выше |
| [Rebuild_Index_SQL] |Индекс columnstore toorebuild SQL для таблицы |

## <a name="causes-of-poor-columnstore-index-quality"></a>Причины низкого качества индекса Columnstore
Если вы определили таблиц с низкой сегмент качеством, требуется tooidentify hello основную причину.  Ниже приведены некоторые основные причины низкого качества сегментов.

1. Нехватка памяти при создании индекса.
2. Высокая интенсивность операций DML.
3. Небольшой объем операций загрузки или потоковые загрузки
4. Слишком много секций

Эти факторы может привести к toohave индекса columnstore значительно меньше, чем hello оптимальной 1 миллион строк на каждую группу строк.  Они также могут вызвать строк toogo toohello разностная группа строк вместо группы сжатая строка. 

### <a name="memory-pressure-when-index-was-built"></a>Нехватка памяти при создании индекса.
Hello количество строк в группе строк в сжатых шире непосредственно связанная toohello строку hello и hello объем памяти, доступной tooprocess hello группы строк.  При строки записываются toocolumnstore таблиц в условиях нехватки памяти, качество сегмента columnstore может упасть.  Таким образом hello рекомендуется toogive hello сеанс, что записи таблицы индекс columnstore tooyour получать доступ к tooas большого объема памяти, как можно.  Так как существует компромисс между памяти и параллелизма, hello рекомендации по правой выделении памяти распределения зависит от данных hello в каждой строке таблицы, сумма hello DWU вы tooyour системы и сумма hello параллелизма гнезд hello может предоставить toohello сеанс, который производит запись данных tooyour таблицы.  По соображениям рекомендуется начинать с xlargerc при использовании DW300 или менее, largerc при использовании DW400 tooDW600 и mediumrc при использовании DW1000 и более поздних версий.

### <a name="high-volume-of-dml-operations"></a>Высокая интенсивность операций DML.
Слишком большое количество операций DML, обновления и удаления строк может привести большей эффективности в hello columnstore. Это особенно важно в тех случаях, когда изменяются hello большую часть строк hello в группе строк.

* Удаление строки из группы сжатая строка логически только помечает строку hello как удаленные. строку Hello остается в группе сжатая строка hello, пока не будет перестроен hello секцию или таблицу.
* Вставка строки добавляет внутренней rowstore hello строки tootooan таблицу с именем разностная группа строк. строки вставлены Hello не преобразованное toocolumnstore до hello разностная группа строк не заполнится и помечен как закрытую. Группы строк будут закрыты после попадания hello максимальную емкость 1 048 576 строк. 
* Обновление строки в формате columnstore обрабатывается как логическое удаление, а затем — как вставка. Hello вставлены строки могут храниться в hello разностного хранилища.

Пакетные обновления и вставки, превышающие порог массового hello 102 400 строк в каждой секции, выровненные распространения будет записывать непосредственно toohello columnstore форматирования. Тем не менее при условии, что равномерное распределение, потребуется изменение более 6.144 миллиона строк в одной операции для этого toooccur toobe. Если hello число строк для данной секции выравниваются распространения является менее 102 400 строк hello переходит toohello разностного хранилища, а также будет находиться там, пока не будет достаточно строк, добавленных или измененных tooclose hello строки группы или hello индекс был перестроен.

### <a name="small-or-trickle-load-operations"></a>Небольшой объем операций загрузки или потоковые загрузки
Небольшие загрузки, поступающие в хранилище данных SQL, иногда называют потоковыми. Обычно они представляют собой near постоянный поток данных полученный системой hello. Тем не менее как этот поток является практически непрерывной hello том строк не особенно большой. Чаще всего hello данных значительно находится ниже порогового значения hello, необходимые для использования в формате toocolumnstore прямую загрузку.

В таких ситуациях она чаще всего лучше tooland hello данных сначала в хранилище больших двоичных объектов и позвольте ему накапливаться предыдущих tooloading. Этот метод часто называют *микропакетной обработкой*.

### <a name="too-many-partitions"></a>Слишком много секций
Другой самое tooconsider — секционирование таблиц кластеризованном влияние hello.  Перед секционированием данные в хранилище данных SQL разбиваются на 60 баз данных.  Во время секционирования выполняется дальнейшее разделение данных.  Если секционирование данных, то вы будете tooconsider, **каждого** toobenefit toohave по крайней мере 1 миллион строк из кластеризованного индекса columnstore потребуется раздела.  Если разбиение таблицы на 100 секций, то таблица будет должны toobenefit toohave по крайней мере 6 миллиарда строк из кластеризованного индекса columnstore (60 распределения * 100 секций * 1 миллион строк). Если таблицу 100 разделов не имеет 6 миллиарда строк, сократите число hello секций или попробуйте вместо таблицы кучи.

После загрузки таблицы с данными выполните hello ниже tooidentify действия и перестройте таблиц с индексами columnstore неоптимальной кластера.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Перестроение индексов tooimprove сегмент качества
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Шаг 1: Определите или создайте пользователя, в которой используется класс ресурса hello
Один быстро tooimmediately повысить качество сегмент — индекс toorebuild hello.  Hello SQL, возвращенный hello над представлением вернет инструкцию ALTER INDEX REBUILD, которая может быть используется toorebuild индексов.  При перестроении индексов, убедитесь, что выделено достаточно памяти toohello сеанс, который будет перестройка индекса.  toodo этого, увеличение hello ресурсов класса пользователя, которая имеет индекс hello toorebuild разрешения в этой таблице toohello рекомендуемые минимальные требования.  Поэтому если пользователь не создано в системе hello, поэтому сначала потребуется toodo Hello класс ресурсов пользователя-владельца базы данных hello нельзя изменить.  Минимальное Hello, мы рекомендуем равно xlargerc при использовании DW300 или менее, largerc при использовании DW400 tooDW600 и mediumrc при использовании DW1000 и более поздних версий.

Ниже приведен пример того, как tooallocate дополнительные пользователя tooa памяти путем увеличения их класса ресурсов.  Дополнительные сведения о классах ресурсов и как toocreate нового пользователя можно найти в hello [параллелизма и рабочей нагрузки управления] [ Concurrency] статьи.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Шаг 2. Перестройка кластеризованных индексов Columnstore, используя пользователя с более высоким классом ресурсов
Вход в качестве hello пользователя из шага 1 (например LoadUser), который теперь с помощью более поздней версии класса ресурсов и выполнение инструкции ALTER INDEX hello.  Убедитесь, что этот пользователь имеет таблиц toohello разрешение ALTER, где происходит перестроение индекса hello.  Эти примеры показывают, как toorebuild hello весь индекс columnstore, а также какие toorebuild одну секцию. Для больших таблиц это более удобным индексы toorebuild одной секции одновременно.

Кроме того, не перестраивая индекс hello, можно скопировать hello таблицы tooa новой таблицы с помощью [CTAS][CTAS].  Какой способ лучше? Для больших объемов данных инструкция [CTAS][CTAS] обычно выполняется быстрее, чем [ALTER INDEX][ALTER INDEX]. Для небольших объемов данных [ALTER INDEX] [ ALTER INDEX] toouse проще и не требует tooswap out hello таблицы.  В разделе **перестроение индексов с CTAS и переключения секций** ниже дополнительные сведения о том, как индексы toorebuild с CTAS.

```sql
-- Rebuild hello entire clustered index
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

В хранилище данных SQL операция перестроения индекса выполняется в автономном режиме.  Дополнительные сведения о перестроении индексов см. в разделе статьи инструкции ALTER INDEX REBUILD hello [дефрагментация индексов Columnstore] [ Columnstore Indexes Defragmentation] и раздел синтаксиса hello [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Шаг 3. Проверка улучшения качества кластеризованных сегментов Columnstore
Повторить запрос hello, которой обозначена таблицы очень плохо сегментирования качества и убедитесь, что сегмент качество улучшилось.  Если не была повысить качество сегмента, возможно hello строки в таблице, лишние широки.  Если для перестроения индексов требуется более высокий объем памяти,

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Перестроение индексов с помощью инструкции CTAS и переключения секций
В этом примере используется [CTAS] [ CTAS] и toorebuild секции таблицы переключения секций. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
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

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Дополнительные сведения о создании секций с помощью повторно `CTAS`, в разделе hello [секции] [ Partition] статьи.

## <a name="next-steps"></a>Дальнейшие действия
toolearn более, статьях hello на [Общие сведения о таблицах][Overview], [типы данных таблицы][Data Types], [распространение таблицы] [ Distribute], [Секционировать таблицу][Partition], [статистики таблицы] [ Statistics] и [ Временные таблицы][Temporary].  toolearn более о рекомендуемых подходах см [рекомендации данных SQL хранилища][SQL Data Warehouse Best Practices].

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
