---
title: "представления aaaUsing T-SQL в хранилище данных SQL Azure | Документы Microsoft"
description: "Советы по использованию представлений Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Представления в хранилище данных SQL
Представления особенно удобны в хранилище данных SQL. Они могут использоваться несколькими различными способами tooimprove hello качества решения.  В этой статье указаны как tooenrich решение с представлениями, а также ограничения hello, которым требуется toobe считается несколько примеров.

> [!NOTE]
> Синтаксис `CREATE VIEW` в этой статье не рассматривается. См. toohello [CREATE VIEW] [ CREATE VIEW] статье на MSDN этот справочные сведения.
> 
> 

## <a name="architectural-abstraction"></a>Архитектурная абстракция
Очень часто модель приложения является toore-создание таблицы с помощью СОЗДАНИЯ таблицы AS ВЫБЕРИТЕ (CTAS) следуют объекта переименование шаблон в процессе загрузки данных.

Приведенный ниже пример Hello добавляет измерения даты tooa новую дату записи. Обратите внимание на то, как новый tabble, DimDate_New, сначала создается и затем переименовали tooreplace hello исходную версию таблицы hello.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Но эти действия могут привести к тому, что таблицы могут появляться в представлении пользователя и исчезать из него; кроме того, могут появляться сообщения об ошибках "Таблица не существует". Представления могут входить пользователи используется tooprovide с уровня согласованного представления одновременным переименовываются hello базовых объектов. Предоставляя пользователям доступ toohello данных через представления, означает, что пользователи не должны toohave видимость hello базовых таблиц. Это обеспечивает целостное взаимодействие с пользователем, можно развивать модель данных hello hello конструкторов хранилищ данных, а добиться максимальной производительности с помощью CTAS во время процесса загрузки данных hello.    

## <a name="performance-optimization"></a>Оптимизация производительности
Представления также может быть загруженные tooenforce оптимизации производительности соединения между таблицами. Например представление можно включить ключ распределения избыточных как часть hello присоединение перемещения данных toominimize критериев.  Еще одним преимуществом представления может быть tooforce определенного запроса или присоединении подсказку. Использование представлений таким образом гарантирует оптимальным образом прибегая hello пользователей tooremember hello правильный конструкция для их соединения всегда выполняются объединения.

## <a name="limitations"></a>Ограничения
Представления в хранилище данных SQL — это только метаданные.  В результате hello следующие параметры будут недоступны.

* Нет возможности привязать схему.
* Не удалось обновить базовой таблицы через представление hello
* Для временных таблиц нельзя создавать представления.
* Не поддерживается для hello EXPAND и NOEXPAND подсказки
* В хранилище данных SQL нет индексированных представлений.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].
Для `CREATE VIEW` синтаксиса см. слишком[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
