---
title: "aaaData типы руководство - хранилище данных SQL Azure | Документы Microsoft"
description: "Рекомендации, что типы данных toodefine совместимы с хранилищем данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a>Руководство по определению типов данных для таблиц в хранилище данных SQL
Используйте следующие рекомендации toodefine табличные типы данных, совместимые с хранилищем данных SQL. Кроме того, toocompatibility, сводя к минимуму размер hello типов данных повышает производительность запросов.

Хранилище данных SQL поддерживает hello наиболее часто используемых типов данных. Список hello поддерживаемых типов данных см. в разделе [типы данных](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) в инструкции CREATE TABLE hello. 


## <a name="minimize-row-length"></a>Уменьшение длины строки
Минимизация hello размер типов данных сокращает hello строку длиной, которая ведет toobetter производительность запросов. Используйте hello наименьший тип данных, работать для реальных данных. 

- Не рекомендуется использовать по умолчанию длинные значения столбцов. Например если hello длинного значения — 25 символов, затем определите столбца как VARCHAR(25). 
- Не нужно использовать [NVARCHAR][NVARCHAR], если вам требуется только VARCHAR.
- По возможности используйте NVARCHAR(4000) или VARCHAR(8000) вместо NVARCHAR(MAX) или VARCHAR(MAX).

При использовании Polybase tooload таблиц, определенных hello длина строки в таблице hello не может превышать 1 МБ. Когда строку с данными переменной длины превышает 1 МБ, можно загрузить строку hello BCP, но не с PolyBase.

## <a name="identify-unsupported-data-types"></a>Определение неподдерживаемых типов данных
Если вы переносите базу данных из другой базы данных SQL, вы можете обнаружить некоторые типы данных, неподдерживаемые в хранилище данных SQL. Используйте типы данных toodiscover неподдерживаемый этого запроса в существующую схему SQL.

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a>Использование обходных решений для неподдерживаемых типов данных

Hello ниже перечислены hello типы данных, хранилище данных SQL не поддерживает и предоставляет альтернативные варианты, которые можно использовать вместо hello неподдерживаемые типы данных.

| Неподдерживаемые типы данных | Возможное решение |
| --- | --- |
| [geometry][geometry] |[varbinary][varbinary] |
| [geography][geography] |[varbinary][varbinary] |
| [hierarchyid][hierarchyid] |[nvarchar][nvarchar](4000) |
| [image][ntext,text,image] |[varbinary][varbinary] |
| [text][ntext,text,image] |[varchar][varchar] |
| [ntext][ntext,text,image] |[nvarchar][nvarchar] |
| [sql_variant][sql_variant] |Разделите столбец на несколько строго типизированных столбцов. |
| [table][table] |Преобразуйте tootemporary таблицы. |
| [timestamp][timestamp] |Переработайте код toouse [datetime2] [ datetime2] и `CURRENT_TIMESTAMP` функции.  По умолчанию поддерживаются только константы, поэтому нельзя использовать current_timestamp как ограничение по умолчанию. Если вам требуется toomigrate значение версии строки с типизированным столбцом отметок времени, используйте [ДВОИЧНЫХ][BINARY](8) или [VARBINARY][BINARY](8) для NOT NULL или Значение NULL, значение версии строки. |
| [xml][xml] |[varchar][varchar] |
| [тип, определенный пользователем][user defined types] |Преобразуйте тип данных в собственном toohello назад по возможности. |
| Значения по умолчанию | Значения по умолчанию поддерживают только литералы и константы.  Недетерминированные выражения или функции, такие как `GETDATE()` или `CURRENT_TIMESTAMP`, не поддерживаются. |


## <a name="next-steps"></a>Дальнейшие действия
toolearn более, см.:

- [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices]
- [Общие сведения о таблицах в хранилище данных SQL][Overview]
- [Распределение таблиц в хранилище данных SQL][Distribute]
- [Индексирование таблиц в хранилище данных SQL][Index]
- [Секционирование таблиц в хранилище данных SQL][Partition]
- [Управление статистикой таблиц в хранилище данных SQL][Statistics]
- [Временные таблицы в хранилище данных SQL][Temporary]

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
