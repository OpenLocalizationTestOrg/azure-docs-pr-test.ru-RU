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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="d129e-103">Использовать запросы tooinstrument метки в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="d129e-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="d129e-104">Хранилище данных SQL поддерживает концепцию так называемых меток.</span><span class="sxs-lookup"><span data-stu-id="d129e-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="d129e-105">Прежде чем углубляться в это понятие, рассмотрим следующий пример.</span><span class="sxs-lookup"><span data-stu-id="d129e-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="d129e-106">Это последняя строка теги «Мой запрос метка» toohello hello строки запроса.</span><span class="sxs-lookup"><span data-stu-id="d129e-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="d129e-107">Это особенно полезно как метка hello запроса, доступ через hello динамических административных представлений.</span><span class="sxs-lookup"><span data-stu-id="d129e-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="d129e-108">Предоставляет механизм tootrack работу проблемных запросов, а также toohelp идентифицировать ход выполнения пакета ETL.</span><span class="sxs-lookup"><span data-stu-id="d129e-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="d129e-109">В данном случае хорошо помогает продуманный способ именования.</span><span class="sxs-lookup"><span data-stu-id="d129e-109">A good naming convention really helps here.</span></span> <span data-ttu-id="d129e-110">Например что-то наподобие "проекта: процедура: инструкции: КОММЕНТАРИЙ" помогает toouniquely идентификатор запроса hello в всем hello кодом в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="d129e-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="d129e-111">toosearch метки, можно использовать следующий запрос, использующий hello hello динамических административных представлений:</span><span class="sxs-lookup"><span data-stu-id="d129e-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="d129e-112">Очень важно wrap квадратные скобки или двойные кавычки вокруг метки слово hello при выполнении запроса.</span><span class="sxs-lookup"><span data-stu-id="d129e-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="d129e-113">Это слово является зарезервированным и в отсутствие разделителей вызывает ошибку.</span><span class="sxs-lookup"><span data-stu-id="d129e-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d129e-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d129e-114">Next steps</span></span>
<span data-ttu-id="d129e-115">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="d129e-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
