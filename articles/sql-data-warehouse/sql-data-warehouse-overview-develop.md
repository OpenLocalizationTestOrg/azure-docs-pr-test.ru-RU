---
title: "aaaResources по разработке хранилища данных в Azure | Документы Microsoft"
description: "Основные понятия разработки, проектные решения, рекомендации и методики программирования для хранилища данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>Проектные решения и методики программирования для хранилища данных SQL
Ознакомьтесь со всеми toobetter понимать эти статьи по разработке ключевых проектных решениях, рекомендации и методики написания кода для хранилища данных SQL.

## <a name="key-design-decisions"></a>Основные проектные решения
Hello ниже статьях выделяет некоторые основные понятия hello и проектные решения, необходимые для разработки hello хранилищу распределенных данных, хранилище данных SQL с помощью toounderstand.

* [подключения][connections];
* [параллелизм][concurrency];
* [транзакции][transactions];
* [пользовательские схемы][user-defined schemas];
* [распределение таблиц][table distribution];
* [индексы таблицы][table indexes];
* [секции таблицы][table partitions];
* [CTAS][CTAS];
* [статистика][statistics].

## <a name="development-recommendations-and-coding-techniques"></a>Рекомендации по разработке и методики программирования
В следующих статьях описаны методики программирования, советы и рекомендации по разработке для хранилища данных SQL:

* [хранимые процедуры][stored procedures];
* [метки][labels];
* [представления][views];
* [временные таблицы][temporary tables];
* [динамический код SQL][dynamic SQL];
* [циклы][looping];
* [группировка по параметрам][group by options];
* [присвоение значения переменной][variable assignment].

## <a name="next-steps"></a>Дальнейшие действия
После через статьи по разработке hello ознакомьтесь со всеми hello [Справочник по Transact-SQL] [ Transact-SQL reference] страницу Дополнительные сведения о синтаксисе hello поддерживается для хранилища данных SQL.

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
