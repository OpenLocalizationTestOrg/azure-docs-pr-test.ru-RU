---
title: "Глоссарий по средствам работы с эластичными базами данных | Документация Майкрософт"
description: "Пояснения к терминам, используемым в средствах работы с эластичными базами данных."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="d007b-103">Глоссарий по средствам работы с эластичными базами данных</span><span class="sxs-lookup"><span data-stu-id="d007b-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="d007b-104">В связи со [средствами работы с эластичными базами данных SQL Azure](sql-database-elastic-scale-introduction.md)применяются следующие термины.</span><span class="sxs-lookup"><span data-stu-id="d007b-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="d007b-105">Для управления [картами сегментов](sql-database-elastic-scale-shard-map-management.md) используются такие инструменты, как [клиентская библиотека](sql-database-elastic-database-client-library.md), [средство разбиения и слияния](sql-database-elastic-scale-overview-split-and-merge.md), [пулы эластичных баз данных](sql-database-elastic-pool.md) и [запросы](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d007b-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="d007b-106">Эти термины используются в статьях [Добавление сегмента с использованием средств эластичных баз данных](sql-database-elastic-scale-add-a-shard.md) и [Устранение проблем сопоставления сегментов с помощью класса RecoveryManager](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d007b-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Термины, используемые в эластичном масштабировании][1]

<span data-ttu-id="d007b-108">**Базы данных**: база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d007b-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="d007b-109">**Маршрутизация, зависящая от данных.** Функциональная возможность, которая позволяет приложению подключаться к сегменту с определенным ключом сегментирования.</span><span class="sxs-lookup"><span data-stu-id="d007b-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="d007b-110">См. статью [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="d007b-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="d007b-111">Сравните с **[многосегментным формированием запросов](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="d007b-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="d007b-112">**Глобальное сопоставление сегментов.** Сопоставление ключей сегментирования и соответствующих сегментов в **наборе сегментов**.</span><span class="sxs-lookup"><span data-stu-id="d007b-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="d007b-113">Глобальная карта сегментов сохраняется в **диспетчере карт сегментов**.</span><span class="sxs-lookup"><span data-stu-id="d007b-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="d007b-114">Сравните с **локальной картой сегментов**.</span><span class="sxs-lookup"><span data-stu-id="d007b-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="d007b-115">**Карта сегментов по списку**: карта сегментов, в которой ключи сегментирования сопоставляются по отдельности.</span><span class="sxs-lookup"><span data-stu-id="d007b-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="d007b-116">Сравните с **сопоставлением сегментов по диапазонам**.</span><span class="sxs-lookup"><span data-stu-id="d007b-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="d007b-117">**Локальная карта сегментов**: хранящаяся в сегменте карта, содержащая сопоставления для шардлетов, расположенных в сегменте.</span><span class="sxs-lookup"><span data-stu-id="d007b-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="d007b-118">**Многосегментное формирование запросов.** Возможность отправлять запросы нескольким сегментам. Наборы результатов возвращаются с использованием семантики UNION ALL (которую также называют "размноженным запросом").</span><span class="sxs-lookup"><span data-stu-id="d007b-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="d007b-119">Сравните с **маршрутизацией, зависящей от данных**.</span><span class="sxs-lookup"><span data-stu-id="d007b-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="d007b-120">**Мультитенантная** и **однотенантная**. Используется для обозначения однотенантной и мультитенантной баз данных.</span><span class="sxs-lookup"><span data-stu-id="d007b-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Однотенантные и мультитенантные базы данных](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="d007b-122">Далее приведено представление **сегментированных** однотенантной и мультитенантной баз данных.</span><span class="sxs-lookup"><span data-stu-id="d007b-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Однотенантные и мультитенантные базы данных](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="d007b-124">**Карта сегментов по диапазонам**: карта сегментов, в которой распределение сегментов осуществляется по нескольким диапазонам смежных значений.</span><span class="sxs-lookup"><span data-stu-id="d007b-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="d007b-125">**Ссылочные таблицы**: таблицы, которые не сегментируются, а реплицируются по сегментам.</span><span class="sxs-lookup"><span data-stu-id="d007b-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="d007b-126">Например, в ссылочной таблице могут храниться почтовые индексы.</span><span class="sxs-lookup"><span data-stu-id="d007b-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="d007b-127">**Сегмент**: база данных SQL Azure, в которой хранятся данные из набора сегментированных данных.</span><span class="sxs-lookup"><span data-stu-id="d007b-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="d007b-128">**Эластичность сегментов.** Возможность **горизонтального** и **вертикального масштабирования**.</span><span class="sxs-lookup"><span data-stu-id="d007b-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="d007b-129">**Сегментированные таблицы**: таблицы, данные которых распределены по сегментам в соответствии со значениями ключей сегментирования.</span><span class="sxs-lookup"><span data-stu-id="d007b-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="d007b-130">**Ключ сегментирования**: значение столбца, который задает принцип распределения данных по сегментам.</span><span class="sxs-lookup"><span data-stu-id="d007b-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="d007b-131">Значения могут принадлежать к следующим типам: **int**, **bigint**, **varbinary** или **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="d007b-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="d007b-132">**Набор сегментов**: коллекция сегментов, которые относятся к одной карте в диспетчере карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="d007b-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="d007b-133">**Шардлет**: все данные, связанные с одним значением ключа сегментирования в сегменте.</span><span class="sxs-lookup"><span data-stu-id="d007b-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="d007b-134">Шардлет — это наименьшая единица возможного переноса данных при перераспределении сегментированных таблиц.</span><span class="sxs-lookup"><span data-stu-id="d007b-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="d007b-135">**Карта сегментов**— это набор сопоставлений ключей сегментирования и соответствующих сегментов.</span><span class="sxs-lookup"><span data-stu-id="d007b-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="d007b-136">**Диспетчер карт сегментов**: объект управления и хранилище данных, в котором содержатся карты сегментов, информация об их местоположении и сопоставления для одного или нескольких наборов сегментов.</span><span class="sxs-lookup"><span data-stu-id="d007b-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Сопоставления][2]

## <a name="verbs"></a><span data-ttu-id="d007b-138">Команды</span><span class="sxs-lookup"><span data-stu-id="d007b-138">Verbs</span></span>
<span data-ttu-id="d007b-139">**Горизонтальное масштабирование**: масштабирование из коллекции сегментов (или в нее) путем добавления или удаления сегментов в карте, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d007b-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Горизонтальное и вертикальное масштабирование][3]

<span data-ttu-id="d007b-141">**Слияние**: перемещение шардлетов из двух сегментов в один и обновление соответствующей карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="d007b-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="d007b-142">**Перемещение шардлетов**: перемещение шардлета в другой сегмент.</span><span class="sxs-lookup"><span data-stu-id="d007b-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="d007b-143">**Сегмент**: горизонтальное секционирование одинаково структурированных данных по нескольким базам данных на основе ключа сегментирования.</span><span class="sxs-lookup"><span data-stu-id="d007b-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="d007b-144">**Разбиение**: перемещение нескольких шардлетов из одного сегмента в другой (как правило, в новый).</span><span class="sxs-lookup"><span data-stu-id="d007b-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="d007b-145">Ключ сегментирования задается пользователем в качестве точки разделения.</span><span class="sxs-lookup"><span data-stu-id="d007b-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="d007b-146">**Вертикальное масштабирование**: масштабирование уровня производительности отдельного сегмента вверх (или вниз).</span><span class="sxs-lookup"><span data-stu-id="d007b-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="d007b-147">Например, перевод сегмента Standard в сегмент Premium (в соответствии с необходимым уровнем производительности).</span><span class="sxs-lookup"><span data-stu-id="d007b-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

