---
title: "Глоссарий инструменты базы данных aaaElastic | Документы Microsoft"
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="6d183-103">Глоссарий по средствам работы с эластичными базами данных</span><span class="sxs-lookup"><span data-stu-id="6d183-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="6d183-104">Hello определяются следующие термины для hello [эластичной базы данных средства](sql-database-elastic-scale-introduction.md), функция базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6d183-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="6d183-105">Hello средства, используемые toomanage [сегмент соответствует](sql-database-elastic-scale-shard-map-management.md)и включать hello [клиентская библиотека](sql-database-elastic-database-client-library.md), hello [средством слияния разбиение](sql-database-elastic-scale-overview-split-and-merge.md), [эластичные пулы](sql-database-elastic-pool.md), и [запросы](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d183-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="6d183-106">Эти термины используются в [Добавление сегментов, с помощью средств эластичной базы данных](sql-database-elastic-scale-add-a-shard.md) и [с помощью проблем карты сегментов toofix классов hello RecoveryManager](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6d183-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Термины, используемые в эластичном масштабировании][1]

<span data-ttu-id="6d183-108">**Базы данных**: база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6d183-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="6d183-109">**Управляемой данными маршрутизацией**: hello функциональность, позволяющую сегментов tooa tooconnect приложения по ключу конкретных сегментирования.</span><span class="sxs-lookup"><span data-stu-id="6d183-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="6d183-110">См. статью [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="6d183-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="6d183-111">Сравнение слишком**[нескольких сегментов запроса](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="6d183-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="6d183-112">**Карта сегментов глобального**: hello сопоставление между ключи сегментирования и их соответствующих сегментов в **набор сегментов**.</span><span class="sxs-lookup"><span data-stu-id="6d183-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="6d183-113">Карта глобального сегментов Hello хранится в hello **диспетчера карты сегментов**.</span><span class="sxs-lookup"><span data-stu-id="6d183-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="6d183-114">Сравнение слишком**карта сегментов локальной**.</span><span class="sxs-lookup"><span data-stu-id="6d183-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="6d183-115">**Карта сегментов по списку**: карта сегментов, в которой ключи сегментирования сопоставляются по отдельности.</span><span class="sxs-lookup"><span data-stu-id="6d183-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="6d183-116">Сравнение слишком**карта сегментов диапазон**.</span><span class="sxs-lookup"><span data-stu-id="6d183-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="6d183-117">**Карта сегментов локальной**: хранятся на сегмент, сопоставление локальных сегментов hello содержит сопоставления для hello подсегментов, которые находятся на hello сегментов.</span><span class="sxs-lookup"><span data-stu-id="6d183-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="6d183-118">**Запрос нескольких сегментов**: hello возможность tooissue запрос к нескольким сегментам, результирующие наборы возвращаются с использованием UNION ALL семантики (также называется «развертываемый запрос»).</span><span class="sxs-lookup"><span data-stu-id="6d183-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="6d183-119">Сравнение слишком**управляемой данными маршрутизацией**.</span><span class="sxs-lookup"><span data-stu-id="6d183-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="6d183-120">**Мультитенантная** и **однотенантная**. Используется для обозначения однотенантной и мультитенантной баз данных.</span><span class="sxs-lookup"><span data-stu-id="6d183-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Однотенантные и мультитенантные базы данных](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="6d183-122">Далее приведено представление **сегментированных** однотенантной и мультитенантной баз данных.</span><span class="sxs-lookup"><span data-stu-id="6d183-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Однотенантные и мультитенантные базы данных](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="6d183-124">**Карта сегментов диапазон**: карта сегментов, в которой hello стратегии распространения сегментов основана на несколько диапазонов непрерывными значениями.</span><span class="sxs-lookup"><span data-stu-id="6d183-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="6d183-125">**Ссылочные таблицы**: таблицы, которые не сегментируются, а реплицируются по сегментам.</span><span class="sxs-lookup"><span data-stu-id="6d183-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="6d183-126">Например, в ссылочной таблице могут храниться почтовые индексы.</span><span class="sxs-lookup"><span data-stu-id="6d183-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="6d183-127">**Сегмент**: база данных SQL Azure, в которой хранятся данные из набора сегментированных данных.</span><span class="sxs-lookup"><span data-stu-id="6d183-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="6d183-128">**Сегмент эластичности**: hello обе возможности tooperform **горизонтальное масштабирование** и **вертикального масштабирования**.</span><span class="sxs-lookup"><span data-stu-id="6d183-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="6d183-129">**Сегментированные таблицы**: таблицы, данные которых распределены по сегментам в соответствии со значениями ключей сегментирования.</span><span class="sxs-lookup"><span data-stu-id="6d183-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="6d183-130">**Ключ сегментирования**: значение столбца, который задает принцип распределения данных по сегментам.</span><span class="sxs-lookup"><span data-stu-id="6d183-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="6d183-131">Hello тип значения может принимать одно из следующих hello: **int**, **bigint**, **varbinary**, или **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="6d183-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="6d183-132">**Набор сегментов**: hello коллекцию сегментов, которые являются атрибутами toohello же карта сегментов в hello диспетчера карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="6d183-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="6d183-133">**Подсегмент**: все данные hello, связанный с одним значением ключа сегментирования в сегмент.</span><span class="sxs-lookup"><span data-stu-id="6d183-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="6d183-134">Подсегмент — наименьшая единица hello перемещения данных возможно при распространении сегментированными таблицами.</span><span class="sxs-lookup"><span data-stu-id="6d183-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="6d183-135">**Карта сегментов**: hello набор сопоставлений между ключи сегментирования и их соответствующих сегментов.</span><span class="sxs-lookup"><span data-stu-id="6d183-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="6d183-136">**Диспетчера карты сегментов**: хранилищем данных и объектов управления, содержащий предшествующей карте сегментов hello, расположения сегментов и сопоставления для одного или нескольких наборов сегментов.</span><span class="sxs-lookup"><span data-stu-id="6d183-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Сопоставления][2]

## <a name="verbs"></a><span data-ttu-id="6d183-138">Команды</span><span class="sxs-lookup"><span data-stu-id="6d183-138">Verbs</span></span>
<span data-ttu-id="6d183-139">**Горизонтальное масштабирование**: hello act масштабирования (или) коллекции сегментов, добавив или удалив карта сегментов tooa сегментов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6d183-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Горизонтальное и вертикальное масштабирование][3]

<span data-ttu-id="6d183-141">**Слияние**: hello Акт перемещение подсегментов из двух сегментов tooone сегментов и обновление карты сегментов hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6d183-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="6d183-142">**Перемещение подсегментов**: hello процесс передачи в одном подсегменте tooa другой сегмент.</span><span class="sxs-lookup"><span data-stu-id="6d183-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="6d183-143">**Сегмент**: hello Акт горизонтального секционирования идентично структурированные данные по нескольким базам данных на основе ключа сегментирования.</span><span class="sxs-lookup"><span data-stu-id="6d183-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="6d183-144">**Разбиение**: hello процесс передачи несколько подсегментов из сегментов (обычно new) tooanother один сегмент.</span><span class="sxs-lookup"><span data-stu-id="6d183-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="6d183-145">Ключ сегментирования предоставляется пользователем hello как hello точкой разбиения.</span><span class="sxs-lookup"><span data-stu-id="6d183-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="6d183-146">**Вертикальное масштабирование**: масштабирование () Акт hello hello отдельный сегмент уровня производительности.</span><span class="sxs-lookup"><span data-stu-id="6d183-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="6d183-147">Например изменение сегмент из стандартных tooPremium (что приводит дополнительные вычислительные ресурсы).</span><span class="sxs-lookup"><span data-stu-id="6d183-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

