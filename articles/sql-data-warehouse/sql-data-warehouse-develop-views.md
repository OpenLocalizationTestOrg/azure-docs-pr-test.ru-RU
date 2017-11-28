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
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="ec98d-103">Представления в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ec98d-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="ec98d-104">Представления особенно удобны в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ec98d-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="ec98d-105">Они могут использоваться несколькими различными способами tooimprove hello качества решения.</span><span class="sxs-lookup"><span data-stu-id="ec98d-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="ec98d-106">В этой статье указаны как tooenrich решение с представлениями, а также ограничения hello, которым требуется toobe считается несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="ec98d-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="ec98d-107">Синтаксис `CREATE VIEW` в этой статье не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="ec98d-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="ec98d-108">См. toohello [CREATE VIEW] [ CREATE VIEW] статье на MSDN этот справочные сведения.</span><span class="sxs-lookup"><span data-stu-id="ec98d-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="ec98d-109">Архитектурная абстракция</span><span class="sxs-lookup"><span data-stu-id="ec98d-109">Architectural abstraction</span></span>
<span data-ttu-id="ec98d-110">Очень часто модель приложения является toore-создание таблицы с помощью СОЗДАНИЯ таблицы AS ВЫБЕРИТЕ (CTAS) следуют объекта переименование шаблон в процессе загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="ec98d-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="ec98d-111">Приведенный ниже пример Hello добавляет измерения даты tooa новую дату записи.</span><span class="sxs-lookup"><span data-stu-id="ec98d-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="ec98d-112">Обратите внимание на то, как новый tabble, DimDate_New, сначала создается и затем переименовали tooreplace hello исходную версию таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="ec98d-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

<span data-ttu-id="ec98d-113">Но эти действия могут привести к тому, что таблицы могут появляться в представлении пользователя и исчезать из него; кроме того, могут появляться сообщения об ошибках "Таблица не существует".</span><span class="sxs-lookup"><span data-stu-id="ec98d-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="ec98d-114">Представления могут входить пользователи используется tooprovide с уровня согласованного представления одновременным переименовываются hello базовых объектов.</span><span class="sxs-lookup"><span data-stu-id="ec98d-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="ec98d-115">Предоставляя пользователям доступ toohello данных через представления, означает, что пользователи не должны toohave видимость hello базовых таблиц.</span><span class="sxs-lookup"><span data-stu-id="ec98d-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="ec98d-116">Это обеспечивает целостное взаимодействие с пользователем, можно развивать модель данных hello hello конструкторов хранилищ данных, а добиться максимальной производительности с помощью CTAS во время процесса загрузки данных hello.</span><span class="sxs-lookup"><span data-stu-id="ec98d-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="ec98d-117">Оптимизация производительности</span><span class="sxs-lookup"><span data-stu-id="ec98d-117">Performance optimization</span></span>
<span data-ttu-id="ec98d-118">Представления также может быть загруженные tooenforce оптимизации производительности соединения между таблицами.</span><span class="sxs-lookup"><span data-stu-id="ec98d-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="ec98d-119">Например представление можно включить ключ распределения избыточных как часть hello присоединение перемещения данных toominimize критериев.</span><span class="sxs-lookup"><span data-stu-id="ec98d-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="ec98d-120">Еще одним преимуществом представления может быть tooforce определенного запроса или присоединении подсказку.</span><span class="sxs-lookup"><span data-stu-id="ec98d-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="ec98d-121">Использование представлений таким образом гарантирует оптимальным образом прибегая hello пользователей tooremember hello правильный конструкция для их соединения всегда выполняются объединения.</span><span class="sxs-lookup"><span data-stu-id="ec98d-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="ec98d-122">Ограничения</span><span class="sxs-lookup"><span data-stu-id="ec98d-122">Limitations</span></span>
<span data-ttu-id="ec98d-123">Представления в хранилище данных SQL — это только метаданные.</span><span class="sxs-lookup"><span data-stu-id="ec98d-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="ec98d-124">В результате hello следующие параметры будут недоступны.</span><span class="sxs-lookup"><span data-stu-id="ec98d-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="ec98d-125">Нет возможности привязать схему.</span><span class="sxs-lookup"><span data-stu-id="ec98d-125">There is no schema binding option</span></span>
* <span data-ttu-id="ec98d-126">Не удалось обновить базовой таблицы через представление hello</span><span class="sxs-lookup"><span data-stu-id="ec98d-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="ec98d-127">Для временных таблиц нельзя создавать представления.</span><span class="sxs-lookup"><span data-stu-id="ec98d-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="ec98d-128">Не поддерживается для hello EXPAND и NOEXPAND подсказки</span><span class="sxs-lookup"><span data-stu-id="ec98d-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="ec98d-129">В хранилище данных SQL нет индексированных представлений.</span><span class="sxs-lookup"><span data-stu-id="ec98d-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec98d-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec98d-130">Next steps</span></span>
<span data-ttu-id="ec98d-131">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="ec98d-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="ec98d-132">Для `CREATE VIEW` синтаксиса см. слишком[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="ec98d-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
