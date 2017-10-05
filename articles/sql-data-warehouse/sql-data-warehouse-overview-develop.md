---
title: "Ресурсы для разработки хранилища данных в Azure | Документация Майкрософт"
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
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="85945-103">Проектные решения и методики программирования для хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="85945-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="85945-104">Ознакомьтесь со статьями о разработке, чтобы лучше понять основные проектные решения, рекомендации и методики программирования для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="85945-104">Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="85945-105">Основные проектные решения</span><span class="sxs-lookup"><span data-stu-id="85945-105">Key design decisions</span></span>
<span data-ttu-id="85945-106">В приведенных ниже статьях описаны основные понятия и проектные решения, с которыми необходимо ознакомиться для разработки распределенного хранилища данных с помощью хранилища данных SQL:</span><span class="sxs-lookup"><span data-stu-id="85945-106">The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="85945-107">[подключения][connections];</span><span class="sxs-lookup"><span data-stu-id="85945-107">[connections][connections]</span></span>
* <span data-ttu-id="85945-108">[параллелизм][concurrency];</span><span class="sxs-lookup"><span data-stu-id="85945-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="85945-109">[транзакции][transactions];</span><span class="sxs-lookup"><span data-stu-id="85945-109">[transactions][transactions]</span></span>
* <span data-ttu-id="85945-110">[пользовательские схемы][user-defined schemas];</span><span class="sxs-lookup"><span data-stu-id="85945-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="85945-111">[распределение таблиц][table distribution];</span><span class="sxs-lookup"><span data-stu-id="85945-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="85945-112">[индексы таблицы][table indexes];</span><span class="sxs-lookup"><span data-stu-id="85945-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="85945-113">[секции таблицы][table partitions];</span><span class="sxs-lookup"><span data-stu-id="85945-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="85945-114">[CTAS][CTAS];</span><span class="sxs-lookup"><span data-stu-id="85945-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="85945-115">[статистика][statistics].</span><span class="sxs-lookup"><span data-stu-id="85945-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="85945-116">Рекомендации по разработке и методики программирования</span><span class="sxs-lookup"><span data-stu-id="85945-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="85945-117">В следующих статьях описаны методики программирования, советы и рекомендации по разработке для хранилища данных SQL:</span><span class="sxs-lookup"><span data-stu-id="85945-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="85945-118">[хранимые процедуры][stored procedures];</span><span class="sxs-lookup"><span data-stu-id="85945-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="85945-119">[метки][labels];</span><span class="sxs-lookup"><span data-stu-id="85945-119">[labels][labels]</span></span>
* <span data-ttu-id="85945-120">[представления][views];</span><span class="sxs-lookup"><span data-stu-id="85945-120">[views][views]</span></span>
* <span data-ttu-id="85945-121">[временные таблицы][temporary tables];</span><span class="sxs-lookup"><span data-stu-id="85945-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="85945-122">[динамический код SQL][dynamic SQL];</span><span class="sxs-lookup"><span data-stu-id="85945-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="85945-123">[циклы][looping];</span><span class="sxs-lookup"><span data-stu-id="85945-123">[looping][looping]</span></span>
* <span data-ttu-id="85945-124">[группировка по параметрам][group by options];</span><span class="sxs-lookup"><span data-stu-id="85945-124">[group by options][group by options]</span></span>
* <span data-ttu-id="85945-125">[присвоение значения переменной][variable assignment].</span><span class="sxs-lookup"><span data-stu-id="85945-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="85945-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85945-126">Next steps</span></span>
<span data-ttu-id="85945-127">После ознакомления со статьями о разработке изучите [справочник по Transact-SQL][Transact-SQL reference], чтобы получить дополнительные сведения о поддерживаемом синтаксисе для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="85945-127">Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.</span></span>

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
