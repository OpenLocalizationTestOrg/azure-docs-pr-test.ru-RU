---
title: "переменные aaaAssign в хранилище данных SQL | Документы Microsoft"
description: "Советы по присваиванию значений переменных Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Назначение переменных в хранилище данных SQL
Переменные в хранилище данных SQL задаются с использованием hello `DECLARE` инструкции или hello `SET` инструкции.

Все следующие hello не вполне допустимые способы tooset значение переменной:

## <a name="setting-variables-with-declare"></a>Задание переменных с помощью DECLARE
Инициализация переменных с DECLARE является одним из наиболее гибкий tooset способов hello значение переменной в хранилище данных SQL.

```sql
DECLARE @v  int = 0
;
```

Также можно использовать более одной переменной DECLARE tooset одновременно. Нельзя использовать `SELECT` или `UPDATE` toodo это:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

Не удается инициализировать и использовать переменную в hello же инструкции DECLARE. tooillustrate hello точке hello приведенном ниже примере показан **не** допускается в качестве @p1 и инициализируется и используется в hello же инструкции DECLARE. Это приведет к ошибке.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Задание значений с помощью SET
SET — это очень распространенный метод задания одной переменной.

Все примеры hello ниже показаны допустимые способы задания переменной с НАБОРОМ:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

С помощью SET можно одновременно задать только одну переменную. Тем не менее, как видно выше, допускаются составные операторы.

## <a name="limitations"></a>Ограничения
Нельзя использовать SELECT или UPDATE, чтобы присвоить значение переменной.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
