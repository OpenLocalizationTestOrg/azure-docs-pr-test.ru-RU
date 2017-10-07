---
title: "aaaCreate суррогатных ключей с использованием идентификатора | Документы Microsoft"
description: "Узнайте, как toouse УДОСТОВЕРЕНИЕ toocreate суррогатные ключи на ваших таблицах."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Создание суррогатных ключей с использованием свойства IDENTITY
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Типы данных][Data Types]
> * [Распределение][Distribute]
> * [Индекс][Index]
> * [Секция][Partition]
> * [Статистика][Statistics]
> * [Временные таблицы][Temporary]
> * [Удостоверение][Identity]
> 
> 

Многие администраторы моделей данных, например toocreate суррогатными ключами на эти таблицы при их разработке моделей хранилища данных. Можно использовать tooachieve свойство IDENTITY hello этой цели просто и эффективно без влияния на производительность нагрузки. 

## <a name="get-started-with-identity"></a>Приступая к работе со свойством IDENTITY
Таблицы можно определить как имеющий свойство IDENTITY hello при первом создании hello таблицы с помощью синтаксиса, аналогичные toohello следующей инструкцией:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

Затем можно использовать `INSERT..SELECT` toopopulate hello таблицы.

## <a name="behavior"></a>Поведение
Hello свойство IDENTITY может спроектированный tooscale out все hello распределения в хранилище данных hello без влияния на производительность нагрузки. Таким образом реализация hello удостоверения ориентирован по достижению этой цели. В этом разделе описываются особенности hello из toohelp реализацию hello понимаете их более подробно.  

### <a name="allocation-of-values"></a>Распределение значений
Hello свойство IDENTITY не гарантирует порядок hello в какой hello распределяются значения символов-заместителей, отображающие hello поведение SQL Server и базы данных SQL Azure. Тем не менее в хранилище данных SQL Azure, гарантирует отсутствие hello более заметно. 

Следующий пример Hello. приведен пример:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

В предыдущих пример hello две строки, приобретенных в распределении 1. Первая строка Hello имеет hello символов-заместителей значение 1 в столбце `C1`, и hello вторая строка имеет значение 61 hello символов-заместителей. Оба эти значения были созданы при hello свойство IDENTITY. Однако hello распределением значений hello не является непрерывным. В этом весь замысел.

### <a name="skewed-data"></a>Неравномерные данные 
диапазон значений для типа данных hello Hello равномерно распределены по hello распределения. Если таблица распространения страдает от становятся ассиметричные данные, затем hello диапазон значений, которые доступны toohello тип данных может быть исчерпана преждевременно. Например, все данные hello в одном распространения заканчивается, затем эффективно hello таблица имеет доступ tooonly sixtieth один hello значений типа данных hello. По этой причине hello свойство IDENTITY ограничено слишком`INT` и `BIGINT` только для типов данных.

### <a name="selectinto"></a>SELECT..INTO
При выборе существующего столбца ИДЕНТИФИКАТОРОВ в новую таблицу hello новый столбец наследует свойство IDENTITY hello, если верно одно из следующих условий hello:
- Hello инструкция SELECT содержит соединение.
- несколько инструкций SELECT соединены с помощью инструкции UNION;
- столбец ИДЕНТИФИКАТОРОВ Hello встречается более одного раза в списке SELECT hello.
- столбец ИДЕНТИФИКАТОРОВ Hello является частью выражения.
    
Если истинно одно из этих условий, hello столбец создается не NULL и не наследует свойство IDENTITY hello.

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
Создание таблицы AS ВЫБЕРИТЕ (CTAS) следующим hello же SQL Server поведение, описанное для SELECT... В. Тем не менее, нельзя указать свойство IDENTITY в определении столбца hello hello `CREATE TABLE` инструкцию hello. Функция IDENTITY hello нельзя использовать в hello `SELECT` частью hello CTAS. toopopulate таблицы необходимо toouse `CREATE TABLE` toodefine hello таблицы, за которым следует `INSERT..SELECT` toopopulate его.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Явная вставка значений в столбец IDENTITY 
Хранилище данных SQL поддерживает синтаксис `SET IDENTITY_INSERT <your table> ON|OFF`. Можно использовать этот синтаксис tooexplicitly вставки значений в столбец ИДЕНТИФИКАТОРОВ hello.

Многие архитекторы данных как стандартные отрицательное toouse для определенных значений строк в их измерений. Пример: hello -1 или строка «неизвестный элемент». 

следующий скрипт Hello показано, как tooexplicitly добавить эту строку с помощью SET IDENTITY_INSERT:

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>Загрузка данных в таблицу со свойством IDENTITY

наличие Hello hello свойство IDENTITY имеет некоторые последствия tooyour загрузка данных код. В этом разделе описываются некоторые основные схемы загрузки данных в таблицы с использованием свойства IDENTITY. 

### <a name="load-data-with-polybase"></a>Загрузка данных с помощью PolyBase
tooload данные в таблицу и создать суррогатный ключ, используя УДОСТОВЕРЕНИЕ, создать таблицу hello и затем использовать инструкции INSERT... SELECT или INSERT... Загрузка hello tooperform значения.

Hello следующий пример выделяет hello базовый шаблон:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> Это не возможные toouse `CREATE TABLE AS SELECT` в настоящее время при загрузке данных в таблицу со столбцом ИДЕНТИФИКАТОРОВ.
> 

Дополнительные сведения о загрузке данных с помощью hello массового копирования программу (BCP) средства см. следующие статьи hello.

- [Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)][]
- [Руководство по использованию PolyBase в хранилище данных SQL][]

### <a name="load-data-with-bcp"></a>Загрузка данных с помощью BCP
Средство командной строки, которые можно использовать tooload данных в хранилище данных SQL является BCP. Один из параметров (-E) элементы управления hello BCP поведение при загрузке данных в таблицу со столбцом ИДЕНТИФИКАТОРОВ. 

Если указан параметр -E, hello значения, которые содержатся в hello входного файла для столбца hello с УДОСТОВЕРЕНИЕМ, сохраняются. Если -E *не* указано, то hello значения в этом столбце учитываются. Если столбец идентификаторов hello не указан, hello данных загружается в обычном режиме. Hello значения создаются политики toohello увеличения и начальное значение свойства hello в соответствии с.

Дополнительные сведения о загрузке данных с помощью команды BCP см. следующие статьи hello:

- [Загрузка данных с помощью bcp][]
- [bcp Utility][] (Служебная программа BCP)

## <a name="catalog-views"></a>Представления каталога
Хранилище данных SQL поддерживает hello `sys.identity_columns` представления каталога. Данное представление может быть используется tooidentify столбца, имеющего свойство IDENTITY hello.

toohelp лучше понять hello схемы базы данных, в этом примере показано, как toointegrate `sys.identity_columns` с другими представлениями каталога системы:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Ограничения
Hello свойство IDENTITY не может использоваться в hello следующие сценарии:
- Когда тип данных столбца hello не INT или BIGINT
- Где hello столбец присутствует также ключ распределения hello
- Где hello таблица является внешней таблицы 

в хранилище данных SQL не поддерживаются следующие функции, связанные с Hello:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Задачи

Этот раздел содержит пример кода можно использовать tooperform общих задач при работе со столбцами ИДЕНТИФИКАТОРОВ.

> [!NOTE] 
> Столбец C1 — hello УДОСТОВЕРЕНИЯ в все hello следующие задачи.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Найти значение hello наибольшим выделенной таблицы
Используйте hello `MAX()` функцию toodetermine hello наибольшее значение выделенной для распределенных таблицы:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Найти hello начального значения и шага приращения для свойства IDENTITY hello
Можно использовать hello каталога представлений toodiscover hello увеличения и начального значения конфигурации значения идентификаторов для таблицы с помощью приветствия при следующем запросе: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Дальнейшие действия

* toolearn Дополнительные сведения о разработке таблиц, в разделе [Общие сведения о таблицах][Overview], [типы табличных данных][Data Types], [распространять таблицы] [ Distribute], [Индекса таблицы][Index], [секционировать таблицу][Partition], и [ Временные таблицы][Temporary]. 
* Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Загрузка данных с помощью bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Руководство по использованию PolyBase в хранилище данных SQL]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[bcp Utility]: https://msdn.microsoft.com/library/ms162802.aspx (Служебная программа BCP)
  

<!--Other Web references-->  
