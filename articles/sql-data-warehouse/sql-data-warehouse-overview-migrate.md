---
title: "aaaMigrate tooSQL вашего решения хранилища данных | Документы Microsoft"
description: "Руководство по миграции для переноса вашей платформы решения tooAzure хранилище данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="145f2-103">Перенос вашего решения tooAzure хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="145f2-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="145f2-104">См. что происходит при переносе существующего tooAzure решения базы данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="145f2-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="145f2-105">Профилирование рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="145f2-105">Profile your workload</span></span>
<span data-ttu-id="145f2-106">Перед миграцией необходимо toobe уверенности, что хранилище данных SQL — hello подходящее решение для рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="145f2-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="145f2-107">Хранилище данных SQL — это распределенная система, предназначенная tooperform анализ больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="145f2-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="145f2-108">Миграция tooSQL хранилища данных требуется некоторые изменения структуры, не слишком жесткие toounderstand, но может занять некоторое время tooimplement.</span><span class="sxs-lookup"><span data-stu-id="145f2-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="145f2-109">Если компании требуется хранилище данных корпоративного уровня, преимущества hello заслуживают hello усилий.</span><span class="sxs-lookup"><span data-stu-id="145f2-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="145f2-110">Однако если не требуется power hello хранилища данных SQL, это более экономичное toouse SQL Server или база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="145f2-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="145f2-111">Рассмотрите возможность использования хранилища данных SQL, если вы:</span><span class="sxs-lookup"><span data-stu-id="145f2-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="145f2-112">обслуживаете один или нескольких терабайтов данных;</span><span class="sxs-lookup"><span data-stu-id="145f2-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="145f2-113">Анализ плана toorun больших объемов данных</span><span class="sxs-lookup"><span data-stu-id="145f2-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="145f2-114">Требуется hello возможность tooscale вычислений и хранения</span><span class="sxs-lookup"><span data-stu-id="145f2-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="145f2-115">Необходимо toosave расходы из-за приостановки вычислительные ресурсы, если они не нужны.</span><span class="sxs-lookup"><span data-stu-id="145f2-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="145f2-116">Не используйте хранилище данных SQL для операционных рабочих нагрузок (OLTP) со следующими характеристиками:</span><span class="sxs-lookup"><span data-stu-id="145f2-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="145f2-117">высокая частота операций чтения и записи;</span><span class="sxs-lookup"><span data-stu-id="145f2-117">High frequency reads and writes</span></span>
- <span data-ttu-id="145f2-118">большое число операций одноэлементной выборки;</span><span class="sxs-lookup"><span data-stu-id="145f2-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="145f2-119">большие объемы операций вставки одной строки;</span><span class="sxs-lookup"><span data-stu-id="145f2-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="145f2-120">необходимость построчной обработки;</span><span class="sxs-lookup"><span data-stu-id="145f2-120">Row by row processing needs</span></span>
- <span data-ttu-id="145f2-121">несовместимые форматы (JSON, XML).</span><span class="sxs-lookup"><span data-stu-id="145f2-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="145f2-122">Планирование миграции hello</span><span class="sxs-lookup"><span data-stu-id="145f2-122">Plan hello migration</span></span>

<span data-ttu-id="145f2-123">После выбора toomigrate tooSQL существующие решения хранилища данных, это миграции hello важные tooplan перед началом работы.</span><span class="sxs-lookup"><span data-stu-id="145f2-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="145f2-124">Одна из целей планирования является tooensure данные схемы таблицы, и ваш код совместимы с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="145f2-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="145f2-125">Существуют некоторые различия совместимости toowork вокруг между текущей системы и хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="145f2-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="145f2-126">Кроме того переноса больших объемов данных tooAzure занимает время.</span><span class="sxs-lookup"><span data-stu-id="145f2-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="145f2-127">Тщательное планирование упростит начало вашей tooAzure данных.</span><span class="sxs-lookup"><span data-stu-id="145f2-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="145f2-128">Планирование другой целью является toomake конструирования tooensure корректировки, которые решение использует преимущества hello высокую производительность запросов, хранилище данных SQL — предназначены tooprovide.</span><span class="sxs-lookup"><span data-stu-id="145f2-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="145f2-129">Проектирование хранилищ данных для масштабирования представлены шаблоны другую структуру и поэтому традиционных подходов не всегда hello наилучшим образом.</span><span class="sxs-lookup"><span data-stu-id="145f2-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="145f2-130">Несмотря на то, что после миграции можно внести некоторые изменения проектирования, изменения раньше в процессе hello будет сэкономить время в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="145f2-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="145f2-131">tooperform успешной миграции, необходимо toomigrate таблицы схемы, кода и данных.</span><span class="sxs-lookup"><span data-stu-id="145f2-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="145f2-132">Рекомендации по этим аспектам переноса можно изучить, воспользовавшись ссылками ниже:</span><span class="sxs-lookup"><span data-stu-id="145f2-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="145f2-133">Перенос схем</span><span class="sxs-lookup"><span data-stu-id="145f2-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="145f2-134">Перенос кода</span><span class="sxs-lookup"><span data-stu-id="145f2-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="145f2-135">[Перенос данных](sql-data-warehouse-migrate-data.md)</span><span class="sxs-lookup"><span data-stu-id="145f2-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="145f2-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="145f2-136">Next steps</span></span>
<span data-ttu-id="145f2-137">также Hello CAT (группа консультантов по) имеет некоторые значительные руководство хранилище данных SQL, в котором они будут публиковать через блоги.</span><span class="sxs-lookup"><span data-stu-id="145f2-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="145f2-138">Рассмотрим их статьи [tooAzure перенос данных хранилища данных SQL на практике] [ Migrating data tooAzure SQL Data Warehouse in practice] Дополнительные рекомендации по миграции.</span><span class="sxs-lookup"><span data-stu-id="145f2-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
