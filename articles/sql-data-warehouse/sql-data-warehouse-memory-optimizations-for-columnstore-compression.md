---
title: "aaaImprove производительности индекса columnstore в Azure SQL | Документы Microsoft"
description: "Уменьшить требования к памяти или увеличьте hello доступной памяти toomaximize hello количество строк индекса columnstore сжимает в каждой группы строк."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Максимальное повышение качества группы строк для индекса columnstore

Качество группы строк определяется hello количество строк в группе строк. Уменьшить требования к памяти или увеличьте hello доступной памяти toomaximize hello количество строк индекса columnstore сжимает в каждой группы строк.  Используйте эти методы tooimprove сжатия и производительности запросов для индексов columnstore.

## <a name="why-hello-rowgroup-size-matters"></a>Важная роль hello размер группы строк
Поскольку индекс columnstore просматривает таблицу путем сканирования сегменты столбцов отдельные группы строк, максимальное увеличение hello количество строк в каждой группе строк повышает производительность запросов. Когда группы строк имеют большое количество строк, сжатие данных повышает, что означает, что имеется меньше tooread данных с диска.

Дополнительные сведения о группах строк см. в [руководстве по индексам сolumnstore](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Целевой размер для групп строк
Для наилучшей производительности запросов hello целью является toomaximize hello число строк для группы строк в индексе columnstore. Группа строк может включать до 1 048 576 строк. Хорошо toonot имеют hello максимальное число строк для группы строк. Индексы columnstore обеспечивают высокую производительность, если группы строк включают хотя бы 100 000 строк.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Группы строк при сжатии можно обрезать

Во время массовой загрузки или columnstore перестроения индекса иногда нет доступных toocompress достаточно памяти, всех hello строки, предназначенные для каждой группы строк. При нехватке памяти, индексы columnstore trim hello размер группы строк, поэтому может быть успешным, сжатия в hello columnstore. 

Если недостаточно памяти toocompress по крайней мере 10 000 строк в каждой группы строк, хранилище данных SQL приведет к ошибке.

Дополнительные сведения о выполнении массовой загрузки см. в статье [Загрузка данных индексов ColumnStore](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Как качество toomonitor группы строк

Динамическое административное Представление (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats), предоставляет полезные сведения, такие как количество строк в группы строк и hello причина усечения, если был обрезки не существует. Можно создать эти сведения tooget динамического административного Представления hello следующие представления в виде tooquery удобным способом для усечения группы строк.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Hello trim_reason_desc сообщает ли hello группы строк был усечен (trim_reason_desc = NO_TRIM подразумевает без обрезания, и группа строк имеет оптимального качества). Hello причин trim указывают преждевременное усечения hello группы строк:
- BULKLOAD: В связи с этим trim используется при hello входящего пакета строк для hello нагрузки было меньше, чем 1 миллион строк. Если существует более 100 000 строк, вставляемых (как противоположность tooinserting в hello разностного хранилища), но наборы hello tooBULKLOAD причина усечения Hello engine создаст группы строк в сжатых. В этом случае можно попробуйте увеличить tooaccumulate окна нагрузки вашего пакета больше строк. Кроме того пересчитать вашей секционирования tooensure схему, не слишком детальные группы строк не может охватывать границы секций.
- MEMORY_LIMITATION: hello engine требуется toocreate групп строк с 1 миллиона строк, определенный объем рабочей памяти. Когда hello загрузки сеанса доступной памяти меньше необходимого hello Работа памяти, группы строк получить преждевременно усекаются. Привет, в следующих разделах объясняется, как tooestimate памяти необходимо выделить больше памяти.
- DICTIONARY_SIZE. Эта причина усечения указывает на то, что усечение групп строк вызвано наличием по крайней мере одного столбца строки с широкими строками и (или) со строками, имеющими большое количество элементов. размер словаря Hello является ограниченной too16, МБ в памяти, и когда этот предел будет достигнут hello группа строк сжимается. При запуске в этом случае рекомендуется отключить hello проблемный столбца в отдельную таблицу.

## <a name="how-tooestimate-memory-requirements"></a>Как tooestimate требования к памяти

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Максимальный объем памяти требуется Hello toocompress одну группу строк — приблизительно

- 72 МБ +
- \#строки \* \#столбцы \* 8 байт +
- \#строки \* \#столбцы коротких строк \* 32 байта +
- \#столбцы длинных строк \* 16 МБ для словаря сжатия

где столбцы коротких строк используют типы строковых данных размером <= 32 байта, а столбцы длинных строк используют типы строковых данных размером > 32 байта.

Используемый метод сжатия длинных строк предназначен для сжатия текста. Этот метод сжатия использует *словарь* toostore текстовых шаблонов. Максимальный размер словаря Hello составляет 16 МБ. Имеется только один словарь для каждого столбца длинной строки в группе строк hello.

Подробные сведения о требованиях к памяти columnstore см. в [видео-руководстве по настройке масштабирования хранилища данных SQL Azure](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Требования к памяти tooreduce способами

Используйте следующие методики требования к памяти tooreduce hello сжатия группы строк в индексах columnstore hello.

### <a name="use-fewer-columns"></a>Используйте меньшее число столбцов
Если это возможно Разрабатывайте hello таблицы с меньшим количеством столбцов. Когда группа строк сжимается в hello columnstore, индекс columnstore hello сжимает каждый сегмент столбца отдельно. Здравствуйте, поэтому требования к памяти toocompress группы строк увеличивается как столбцы увеличения количества hello.


### <a name="use-fewer-string-columns"></a>Используйте меньшее число строковых столбцов
Столбцы строковых типов данных требуют больше памяти, чем числовые типы и типы даты. требования к памяти tooreduce, рассмотрите возможность удаления строковых столбцов из таблицы фактов и разместив их в небольших таблиц измерений.

Дополнительные требования к памяти при сжатии строк:

- Копирование символов too32 строковых данных может потребовать 32 байта дополнительные каждого значения.
- строковые типы данных свыше 32 символов сжимаются с помощью методов словаря,  Каждый столбец в группе строк hello, может потребоваться копирование tooan дополнительных 16 МБ toobuild hello словарей.

### <a name="avoid-over-partitioning"></a>Избегайте избыточного секционирования

Индексы columnstore создают одну или несколько групп строк в каждой секции. В хранилище данных SQL hello количество секций быстро увеличивается из-за распределения данных hello и каждого распределения секционирована. Если таблица hello содержит слишком много секций, могут не существовать rowgroups hello toofill достаточное количество строк. отсутствие Hello строк, вызывают нехватку памяти во время сжатия, но приводит toorowgroups, не произойдет hello наилучшую производительность запросов columnstore.

Другой причине tooavoid чрезмерно секционирования является памяти затраты для загрузки строк в индекс columnstore на секционированной таблице. При загрузке большого числа секций может получать hello входящих строк, которые хранятся в памяти, пока каждая секция имеет достаточно toobe строк сжаты. Слишком большое число секций приводит к избыточному потреблению памяти.

### <a name="simplify-hello-load-query"></a>Упростите запрос загрузки hello

Hello базы данных общих папок hello предоставления памяти для запроса среди всех операторов hello в запросе hello. Если загрузить запрос имеет сложную сортировку и соединения, уменьшается hello памяти, доступный для сжатия.

Проектирование hello toofocus запросов нагрузки только на загрузке запроса hello. Если вам требуется toorun преобразований данных hello, запускайте их отдельно от hello нагрузки запроса. Например данные hello этап таблицы кучи, запуска преобразований hello и затем загружать hello промежуточной таблицы в индекс columnstore hello. Можно также сначала загрузить данные hello и затем использовать hello MPP системы tootransform hello данные.

### <a name="adjust-maxdop"></a>Настройка MAXDOP

Каждого распределения сжимает группы строк в columnstore hello в параллельном режиме, при наличии более чем одного ядра ЦП, доступных для распространения. параллелизм Hello требует дополнительных ресурсов памяти, что может привести нехватка toomemory и усечения строк.

hello MAXDOP запроса указание tooforce hello нагрузки операции toorun tooreduce нехватки памяти, можно использовать в последовательном режиме внутри каждого распределения.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Способы tooallocate больший объем памяти

DWU размер и hello класс пользовательских ресурсов вместе определяют, какой объем памяти доступен для запроса пользователя. tooincrease hello памяти предоставить для загрузки запроса, можно увеличить число hello Dwu или увеличить hello класс ресурсов.

- . в разделе hello tooincrease Dwu, [как масштабировать производительность?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- Класс ресурсов hello toochange для запроса, в разделе [измените пример класса ресурса для пользователя](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Например на DWU 100 пользователь в классе ресурса smallrc hello может использовать 100 МБ памяти для каждого распределения. Hello Подробнее [параллелизма в хранилище данных SQL](sql-data-warehouse-develop-concurrency.md).

Предположим, что определить необходимость 700 МБ размер группы строк высокого качества tooget памяти. Эти примеры показывают, как можно выполнить запрос hello нагрузки с достаточным объемом памяти.

- При наличии DWU 1000 и mediumrc выделение памяти составит 800 МБ.
- При наличии DWU 600 и largerc выделение памяти составит 800 МБ.


## <a name="next-steps"></a>Дальнейшие действия

toofind большую производительность tooimprove способами, в хранилище данных SQL, в разделе hello [Обзор производительности](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
