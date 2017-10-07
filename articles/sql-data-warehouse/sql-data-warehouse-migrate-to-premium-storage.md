---
title: "aaaMigrate toopremium хранилища в хранилище Azure существующих данных | Документы Microsoft"
description: "Инструкции по переносу существующих toopremium хранилища данных"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Перенос toopremium хранение данных
В хранилище данных SQL Azure недавно реализована возможность использовать [хранилище класса Premium, чтобы обеспечить более предсказуемую производительность][premium storage for greater performance predictability]. Существующие данные складов в настоящее время в стандартном хранилище теперь могут быть перенесены toopremium хранилища. Можно воспользоваться преимуществами автоматическая миграция, или если вы предпочитаете toocontrol при toomigrate (которая включает в себя некоторое время простоя), можно сделать самостоятельно hello миграции.

Если имеется более одного хранилища данных, используйте hello [расписание автоматического переноса] [ automatic migration schedule] toodetermine, когда следует выполнять миграцию.

## <a name="determine-storage-type"></a>Определение типа хранилища
При создании хранилища данных перед hello после даты, используемой в текущий момент стандартное хранилище.

| **Регион** | **Хранилище данных, созданное до указанной даты** |
|:--- |:--- |
| Восточная часть Австралии |Хранилище класса Premium пока недоступно |
| Восток Китая |1 ноября 2016 г. |
| Север Китая |1 ноября 2016 г. |
| Центральная Германия |1 ноября 2016 г. |
| Северо-восточная Германия |1 ноября 2016 г. |
| Западная Индия |Хранилище класса Premium пока недоступно |
| Западная часть Японии |Хранилище класса Premium пока недоступно |
| Северо-центральный регион США |10 ноября 2016 г. |

## <a name="automatic-migration-details"></a>Сведения об автоматической миграции
По умолчанию, мы перенесем базы данных автоматически между 6:00 и 6:00:00 по местному времени для своего региона во время hello [расписание автоматического переноса][automatic migration schedule]. Хранилище данных будет невозможно использовать во время миграции hello. Hello миграции занимает примерно один час в расчете на терабайт хранилища в хранилище данных. Вы не будете платить во время любой части hello автоматическую миграцию.

> [!NOTE]
> После завершения переноса hello, хранилищем данных будет снова документации и может использоваться.
>
>

Корпорация Майкрософт занимает hello следующие шаги toocomplete hello миграции (эти файлы не требуют любой вмешательства со стороны пользователя). В этом примере мы рассмотрим существующее хранилище данных с именем MyDW, размещенное в хранилище класса Standard.

1. Microsoft переименовывает «MyDW» слишком «MyDW_DO_NOT_USE_ [Timestamp]».
2. Корпорация Майкрософт приостанавливает MyDW_DO_NOT_USE_[метка_времени]. В это время создается резервная копия. Этот процесс может быть несколько раз приостановлен и возобновлен, если возникнут какие-либо проблемы.
3. Корпорация Майкрософт создает новое хранилище данных с именем «MyDW» в хранилище класса premium из резервной копии hello в шаге 2. «MyDW» появятся только после завершения восстановления hello.
4. После завершения восстановления hello, «MyDW» возвращает toohello и тех же данных в хранилище единицы и состоянии (или приостановлено), которое было до миграции hello.
5. После завершения миграции hello Майкрософт удалит «MyDW_DO_NOT_USE_ [Timestamp]».

> [!NOTE]
> Hello следующие параметры не переносятся в ходе миграции hello:
>
> * Аудит на уровне базы данных hello должен снова включить toobe.
> * Правила брандмауэра на уровне базы данных hello должны toobe повторно добавлены. Правила брандмауэра на уровне сервера hello не затрагиваются.
>
>

### <a name="automatic-migration-schedule"></a>расписание автоматического переноса
Автоматическая миграция период между 6:00 и 6:00:00 (местное время в одном регионе) hello, после отключения расписания.

| **Регион** | **Предполагаемая дата начала** | **Предполагаемая дата окончания** |
|:--- |:--- |:--- |
| Восточная часть Австралии |Еще не определено |Еще не определено |
| Восток Китая |9 января 2017 г. |13 января 2017 г. |
| Север Китая |9 января 2017 г. |13 января 2017 г. |
| Центральная Германия |9 января 2017 г. |13 января 2017 г. |
| Северо-восточная Германия |9 января 2017 г. |13 января 2017 г. |
| Западная Индия |Еще не определено |Еще не определено |
| Западная часть Японии |Еще не определено |Еще не определено |
| Северо-центральный регион США |9 января 2017 г. |13 января 2017 г. |

## <a name="self-migration-toopremium-storage"></a>Хранилище toopremium самостоятельной миграции
Если требуется toocontrol, когда произойдет время простоя, можно использовать следующие шаги toomigrate существующее хранилище данных в стандартном хранилище toopremium хранилище hello. Если этот параметр выбран, hello самостоятельной миграции необходимо выполнить перед началом миграции автоматического hello в этом регионе. Это гарантирует, что позволяет избежать риска hello автоматическую миграцию, вызывающем конфликт (см. toohello [расписание автоматического переноса][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Инструкции по самостоятельной миграции
toomigrate данные в хранилище самостоятельно, hello архивирования и восстановления использовать функции. Hello восстановления миграции hello представлена ожидаемый tootake от часа за терабайт хранилища в хранилище данных. Hello tookeep одинаковые имена, после завершения миграции, выполните hello [toorename действия во время миграции][steps toorename during migration].

1. [Приостановите работу][Pause] хранилища данных. При этом будет выполнено автоматическое резервное копирование.
2. [Восстановите][Restore] данные из последнего моментального снимка.
3. Удалите имеющееся хранилище данных, размещенное в хранилище класса Standard. **Если этот шаг не toodo, будет взиматься плата за обоих хранилищах данных.**

> [!NOTE]
> Hello следующие параметры не переносятся в ходе миграции hello:
>
> * Аудит на уровне базы данных hello должен снова включить toobe.
> * Правила брандмауэра на уровне базы данных hello должны toobe повторно добавлены. Правила брандмауэра на уровне сервера hello не затрагиваются.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Переименуйте хранилище данных во время переноса (необязательно)
Две базы данных на hello на одном логическом сервере не может иметь hello таким же именем. Хранилище данных SQL теперь поддерживает возможность hello toorename хранилища данных.

В этом примере мы рассмотрим существующее хранилище данных с именем MyDW, размещенное в хранилище класса Standard.

1. Переименуйте «MyDW» hello, выполнив команду ALTER DATABASE. (В этом примере мы будем переименованием «MyDW_BeforeMigration.»)  Эта команда останавливает все существующие транзакции и должна быть выполнена в toosucceed hello базы данных master.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Приостановите работу][Pause] хранилища MyDW_BeforeMigration. При этом будет выполнено автоматическое резервное копирование.
3. [Восстановление] [ Restore] из самый последний моментальный снимок новой базы данных с именем hello он используется toobe (например, «MyDW»).
4. Удалите хранилище данных MyDW_BeforeMigration. **Если этот шаг не toodo, будет взиматься плата за обоих хранилищах данных.**


## <a name="next-steps"></a>Дальнейшие действия
С hello изменить toopremium хранилище, необходимо также создать требуется увеличение количества файлов больших двоичных объектов базы данных в hello базовой архитектуры хранилища данных. выигрыш в производительности hello toomaximize этого изменения перестройке кластеризованных индексов с помощью hello, выполнив сценарий. Hello скрипт работает путем принудительного некоторые из существующих данных toohello дополнительных BLOB-объектов. Если не предпринимать никаких действий, данных Здравствуй естественным образом будет распространять со временем как загрузить дополнительные данные в таблицах.

**Предварительные требования:**

- Hello хранилище данных следует запускать с единицами измерения хранилища данных 1000 или более поздней версии (в разделе [шкалы вычислительная мощность][scale compute power]).
- Hello пользователь, выполняющий скрипт hello должно быть в hello [роли mediumrc] [ mediumrc role] или более поздней версии. tooadd toothis роль пользователя выполнить hello ниже:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Если возникли проблемы с хранилищу данных [создать обращение в службу поддержки] [ create a support ticket] и ссылаться на «хранилище миграции toopremium» как hello из возможных причин.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
