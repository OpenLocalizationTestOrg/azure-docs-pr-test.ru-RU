---
title: "aaaUse метки tooinstrument запросов в хранилище данных SQL | Документы Microsoft"
description: "Советы по использованию метки tooinstrument запросов в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Использовать запросы tooinstrument метки в хранилище данных SQL
Хранилище данных SQL поддерживает концепцию так называемых меток. Прежде чем углубляться в это понятие, рассмотрим следующий пример.

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Это последняя строка теги «Мой запрос метка» toohello hello строки запроса. Это особенно полезно как метка hello запроса, доступ через hello динамических административных представлений. Предоставляет механизм tootrack работу проблемных запросов, а также toohelp идентифицировать ход выполнения пакета ETL.

В данном случае хорошо помогает продуманный способ именования. Например что-то наподобие "проекта: процедура: инструкции: КОММЕНТАРИЙ" помогает toouniquely идентификатор запроса hello в всем hello кодом в системе управления версиями.

toosearch метки, можно использовать следующий запрос, использующий hello hello динамических административных представлений:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> Очень важно wrap квадратные скобки или двойные кавычки вокруг метки слово hello при выполнении запроса. Это слово является зарезервированным и в отсутствие разделителей вызывает ошибку.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
