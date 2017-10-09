---
title: "Управление aaaConcurrency и рабочей нагрузки в хранилище данных SQL | Документы Microsoft"
description: "Общие сведения управлении параллелизмом и рабочей нагрузкой в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="9db61-103">Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="9db61-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="9db61-104">toodeliver прогнозируемую производительность в масштабе, хранилище данных SQL Microsoft Azure помогает управлять уровней параллелизма и распределение ресурсов, таких как память и определения приоритетов ЦП.</span><span class="sxs-lookup"><span data-stu-id="9db61-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="9db61-105">В этой статье понятия вы toohello управление параллелизмом и рабочей нагрузки, объясняется, как обе эти функции были реализованы и как ими можно было управлять в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="9db61-106">Управление рабочими нагрузками хранилище данных SQL — предполагаемого toohelp поддержки многопользовательских средах.</span><span class="sxs-lookup"><span data-stu-id="9db61-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="9db61-107">но не поддерживает мультитенантные рабочие нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9db61-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="9db61-108">Пределы параллелизма</span><span class="sxs-lookup"><span data-stu-id="9db61-108">Concurrency limits</span></span>
<span data-ttu-id="9db61-109">Хранилище данных SQL позволяет вверх too1 024 одновременных подключений.</span><span class="sxs-lookup"><span data-stu-id="9db61-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="9db61-110">Все эти подключения могут одновременно отправлять запросы.</span><span class="sxs-lookup"><span data-stu-id="9db61-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="9db61-111">Однако toooptimize пропускной способности, хранилище данных SQL может поставить в очередь tooensure некоторые запросы, что каждый запрос получает инструкции grant минимальный объем памяти.</span><span class="sxs-lookup"><span data-stu-id="9db61-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="9db61-112">Постановка в очередь происходит во время выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="9db61-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="9db61-113">По очереди запросов при параллелизма заполнится до предела, хранилище данных SQL можно увеличить общая пропускная способность за счет того, активных запросов get доступа toocritically необходимые ресурсы памяти.</span><span class="sxs-lookup"><span data-stu-id="9db61-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="9db61-114">Предельные границы параллелизма в хранилище данных SQL зависят от двух значений: *количества одновременных запросов* и *количества слотов выдачи*.</span><span class="sxs-lookup"><span data-stu-id="9db61-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="9db61-115">Для tooexecute запроса она должна выполняться в рамках hello предельное число параллелизма и выделение слота hello параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="9db61-116">Параллельных запросов являются запросами hello, выполнению в hello же время.</span><span class="sxs-lookup"><span data-stu-id="9db61-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="9db61-117">Хранилище данных SQL поддерживает до too32 параллельных запросов на больших размеров DWU hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="9db61-118">Слоты выдачи выделяются на основе DWU.</span><span class="sxs-lookup"><span data-stu-id="9db61-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="9db61-119">Каждые 100 DWU обеспечивают 4 слота.</span><span class="sxs-lookup"><span data-stu-id="9db61-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="9db61-120">Например, для DW100 выделяется 4 слота, а для DW1000 — 40 слотов.</span><span class="sxs-lookup"><span data-stu-id="9db61-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="9db61-121">Каждый запрос использует один или несколько параллелизма разъемов, зависящее от hello [класс ресурсов](#resource-classes) hello запроса.</span><span class="sxs-lookup"><span data-stu-id="9db61-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="9db61-122">Запросы, выполняемые в классе ресурса smallrc hello используют один слот параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="9db61-123">Запросы, выполняемые с более высоким классом ресурсов, будут использовать больше слотов выдачи.</span><span class="sxs-lookup"><span data-stu-id="9db61-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="9db61-124">Hello следующей таблице описываются ограничения hello для параллельных запросов и слотов параллелизма в hello различных размеров DWU.</span><span class="sxs-lookup"><span data-stu-id="9db61-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="9db61-125">Пределы параллелизма</span><span class="sxs-lookup"><span data-stu-id="9db61-125">Concurrency limits</span></span>
| <span data-ttu-id="9db61-126">DWU</span><span class="sxs-lookup"><span data-stu-id="9db61-126">DWU</span></span> | <span data-ttu-id="9db61-127">Максимальное число одновременных запросов</span><span class="sxs-lookup"><span data-stu-id="9db61-127">Max concurrent queries</span></span> | <span data-ttu-id="9db61-128">Число выделенных слотов выдачи</span><span class="sxs-lookup"><span data-stu-id="9db61-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="9db61-129">DW100</span><span class="sxs-lookup"><span data-stu-id="9db61-129">DW100</span></span> |<span data-ttu-id="9db61-130">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-130">4</span></span> |<span data-ttu-id="9db61-131">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-131">4</span></span> |
| <span data-ttu-id="9db61-132">DW200</span><span class="sxs-lookup"><span data-stu-id="9db61-132">DW200</span></span> |<span data-ttu-id="9db61-133">8</span><span class="sxs-lookup"><span data-stu-id="9db61-133">8</span></span> |<span data-ttu-id="9db61-134">8</span><span class="sxs-lookup"><span data-stu-id="9db61-134">8</span></span> |
| <span data-ttu-id="9db61-135">DW300</span><span class="sxs-lookup"><span data-stu-id="9db61-135">DW300</span></span> |<span data-ttu-id="9db61-136">12</span><span class="sxs-lookup"><span data-stu-id="9db61-136">12</span></span> |<span data-ttu-id="9db61-137">12</span><span class="sxs-lookup"><span data-stu-id="9db61-137">12</span></span> |
| <span data-ttu-id="9db61-138">DW400</span><span class="sxs-lookup"><span data-stu-id="9db61-138">DW400</span></span> |<span data-ttu-id="9db61-139">16</span><span class="sxs-lookup"><span data-stu-id="9db61-139">16</span></span> |<span data-ttu-id="9db61-140">16</span><span class="sxs-lookup"><span data-stu-id="9db61-140">16</span></span> |
| <span data-ttu-id="9db61-141">DW500</span><span class="sxs-lookup"><span data-stu-id="9db61-141">DW500</span></span> |<span data-ttu-id="9db61-142">20</span><span class="sxs-lookup"><span data-stu-id="9db61-142">20</span></span> |<span data-ttu-id="9db61-143">20</span><span class="sxs-lookup"><span data-stu-id="9db61-143">20</span></span> |
| <span data-ttu-id="9db61-144">DW600</span><span class="sxs-lookup"><span data-stu-id="9db61-144">DW600</span></span> |<span data-ttu-id="9db61-145">24</span><span class="sxs-lookup"><span data-stu-id="9db61-145">24</span></span> |<span data-ttu-id="9db61-146">24</span><span class="sxs-lookup"><span data-stu-id="9db61-146">24</span></span> |
| <span data-ttu-id="9db61-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="9db61-147">DW1000</span></span> |<span data-ttu-id="9db61-148">32</span><span class="sxs-lookup"><span data-stu-id="9db61-148">32</span></span> |<span data-ttu-id="9db61-149">40</span><span class="sxs-lookup"><span data-stu-id="9db61-149">40</span></span> |
| <span data-ttu-id="9db61-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="9db61-150">DW1200</span></span> |<span data-ttu-id="9db61-151">32</span><span class="sxs-lookup"><span data-stu-id="9db61-151">32</span></span> |<span data-ttu-id="9db61-152">48</span><span class="sxs-lookup"><span data-stu-id="9db61-152">48</span></span> |
| <span data-ttu-id="9db61-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="9db61-153">DW1500</span></span> |<span data-ttu-id="9db61-154">32</span><span class="sxs-lookup"><span data-stu-id="9db61-154">32</span></span> |<span data-ttu-id="9db61-155">60</span><span class="sxs-lookup"><span data-stu-id="9db61-155">60</span></span> |
| <span data-ttu-id="9db61-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="9db61-156">DW2000</span></span> |<span data-ttu-id="9db61-157">32</span><span class="sxs-lookup"><span data-stu-id="9db61-157">32</span></span> |<span data-ttu-id="9db61-158">80</span><span class="sxs-lookup"><span data-stu-id="9db61-158">80</span></span> |
| <span data-ttu-id="9db61-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="9db61-159">DW3000</span></span> |<span data-ttu-id="9db61-160">32</span><span class="sxs-lookup"><span data-stu-id="9db61-160">32</span></span> |<span data-ttu-id="9db61-161">120</span><span class="sxs-lookup"><span data-stu-id="9db61-161">120</span></span> |
| <span data-ttu-id="9db61-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="9db61-162">DW6000</span></span> |<span data-ttu-id="9db61-163">32</span><span class="sxs-lookup"><span data-stu-id="9db61-163">32</span></span> |<span data-ttu-id="9db61-164">240</span><span class="sxs-lookup"><span data-stu-id="9db61-164">240</span></span> |

<span data-ttu-id="9db61-165">При достижении одного из этих пороговых значений, новые запросы помещаются в очередь и выполняются в порядке поступления.</span><span class="sxs-lookup"><span data-stu-id="9db61-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="9db61-166">Завершения запросов и число запросов и слоты hello упадет ниже ограничения hello, освобождаются в очереди запросов.</span><span class="sxs-lookup"><span data-stu-id="9db61-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="9db61-167">*Выберите* запросов, выполняющихся исключительно на динамические административные представления (DMV) или каким-либо ограничения параллелизма hello не определены представления каталога.</span><span class="sxs-lookup"><span data-stu-id="9db61-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="9db61-168">Вы можете отслеживать hello системы независимо от hello число запросов, выполняющихся на нем.</span><span class="sxs-lookup"><span data-stu-id="9db61-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="9db61-169">Классы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-169">Resource classes</span></span>
<span data-ttu-id="9db61-170">Ресурс классов помогают контролировать выделения памяти и ЦП с данным запросом tooa.</span><span class="sxs-lookup"><span data-stu-id="9db61-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="9db61-171">Можно назначить два вида ресурсов классы tooa пользователя в форме hello ролей базы данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="9db61-172">Существуют следующие два типа ресурсов классов Hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="9db61-173">Классы динамических ресурсов (**smallrc mediumrc, largerc xlargerc**) выделить переменный объем памяти в зависимости от hello текущей DWU.</span><span class="sxs-lookup"><span data-stu-id="9db61-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="9db61-174">Это означает, что при вертикальном масштабировании tooa больше DWU запросы, автоматически получают больший объем памяти.</span><span class="sxs-lookup"><span data-stu-id="9db61-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="9db61-175">Статические классы ресурсов (**staticrc10 staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) выделить hello такого же объема памяти, вне зависимости от hello текущей DWU (при условии, что hello DWU сам располагает достаточным объемом памяти).</span><span class="sxs-lookup"><span data-stu-id="9db61-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="9db61-176">Это означает, что при большем значении DWU, можно выполнить дополнительные запросы в каждом классе ресурсов одновременно.</span><span class="sxs-lookup"><span data-stu-id="9db61-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="9db61-177">Для пользователей, использующих класс ресурсов **smallrc** и **staticrc10**, выделяется меньший объем памяти, и предоставляются большие возможности параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="9db61-178">Напротив, пользователям назначены слишком**xlargerc** или **staticrc80** получают большой объем памяти, и поэтому меньше их запросы могут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="9db61-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="9db61-179">По умолчанию каждый пользователь является членом класса hello небольшой ресурсов **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="9db61-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="9db61-180">Здравствуйте, процедура `sp_addrolemember` — используется класс ресурса со tooincrease hello и `sp_droprolemember` — используется класс ресурсов toodecrease hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="9db61-181">Например, эта команда увеличивает класс ресурсов hello объекта loaduser слишком**largerc**:</span><span class="sxs-lookup"><span data-stu-id="9db61-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="9db61-182">Запросы, которые не учитывают классы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="9db61-183">Существует несколько типов запросов, которые не смогут воспользоваться преимуществами большего выделения памяти.</span><span class="sxs-lookup"><span data-stu-id="9db61-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="9db61-184">Hello система игнорирует их класс выделения ресурсов и всегда вместо выполнения этих запросов в классе hello мало ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="9db61-185">Если эти запросы всегда выполняются в классе мало ресурсов hello, они могут выполняться, когда ячеек с параллелизмом, при недостатке свободной и они не будет использовать дополнительные слоты, чем требуется.</span><span class="sxs-lookup"><span data-stu-id="9db61-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="9db61-186">Дополнительные сведения см. в разделе [Исключения для запросов в отношении ограничений параллелизма](#query-exceptions-to-concurrency-limits).</span><span class="sxs-lookup"><span data-stu-id="9db61-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="9db61-187">Дополнительные сведения о назначении классов ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-187">Details on resource class assignment</span></span>


<span data-ttu-id="9db61-188">Ниже приведены дополнительные сведения о классах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-188">A few more details on resource class:</span></span>

* <span data-ttu-id="9db61-189">*Изменение роли* требуется разрешение toochange hello ресурсов класса пользователя.</span><span class="sxs-lookup"><span data-stu-id="9db61-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="9db61-190">Несмотря на то, что можно добавить tooone пользователя или более высокие классы ресурсов hello, динамический ресурс классы имеют приоритет над классы статический ресурс.</span><span class="sxs-lookup"><span data-stu-id="9db61-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="9db61-191">То есть если пользователю назначено tooboth **mediumrc**(динамически) и **staticrc80**(статический), **mediumrc** — класс ресурсов hello, учитывается.</span><span class="sxs-lookup"><span data-stu-id="9db61-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="9db61-192">При назначении пользователю toomore, чем класс один ресурс в типе класса конкретный ресурс (более одного класса динамический ресурс или несколько классов статический ресурс), принимается класс ресурсов наибольший hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="9db61-193">То есть если пользователю назначено tooboth mediumrc и largerc, учитывается выше hello класс ресурсов (largerc).</span><span class="sxs-lookup"><span data-stu-id="9db61-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="9db61-194">И, если пользователю назначено tooboth **staticrc20** и **statirc80**, **staticrc80** обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="9db61-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="9db61-195">Класс ресурсов Hello hello системы администрирования пользователя нельзя.</span><span class="sxs-lookup"><span data-stu-id="9db61-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="9db61-196">Подробное описание примера см. в разделе [Пример изменения класса ресурсов пользователя](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="9db61-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="9db61-197">Выделение памяти</span><span class="sxs-lookup"><span data-stu-id="9db61-197">Memory allocation</span></span>
<span data-ttu-id="9db61-198">Существуют преимущества и недостатки tooincreasing класс ресурса пользователя.</span><span class="sxs-lookup"><span data-stu-id="9db61-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="9db61-199">Увеличение класс ресурсов для пользователя, предоставляет их запросы доступа toomore памяти, что может означать, что запросы выполняются быстрее.</span><span class="sxs-lookup"><span data-stu-id="9db61-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="9db61-200">Однако классы более высокого ресурсов также уменьшить hello числа параллельных запросов, которые могут выполняться.</span><span class="sxs-lookup"><span data-stu-id="9db61-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="9db61-201">Это hello компромисса между выделения больших объемов памяти tooa одного запроса или разрешить другие запросы, которые также должны распределения памяти, toorun одновременно.</span><span class="sxs-lookup"><span data-stu-id="9db61-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="9db61-202">Если один пользователь имеет высокий уровень выделение памяти для запроса, другие пользователи не получат доступ toothat же toorun памяти запроса.</span><span class="sxs-lookup"><span data-stu-id="9db61-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="9db61-203">в следующей таблице Hello сопоставляет hello память, выделенную распространения tooeach DWU и ресурсов класса.</span><span class="sxs-lookup"><span data-stu-id="9db61-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="9db61-204">Выделение памяти на распределение для классов динамических ресурсов (в МБ)</span><span class="sxs-lookup"><span data-stu-id="9db61-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="9db61-205">DWU</span><span class="sxs-lookup"><span data-stu-id="9db61-205">DWU</span></span> | <span data-ttu-id="9db61-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="9db61-206">smallrc</span></span> | <span data-ttu-id="9db61-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="9db61-207">mediumrc</span></span> | <span data-ttu-id="9db61-208">largerc</span><span class="sxs-lookup"><span data-stu-id="9db61-208">largerc</span></span> | <span data-ttu-id="9db61-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="9db61-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="9db61-210">DW100</span><span class="sxs-lookup"><span data-stu-id="9db61-210">DW100</span></span> |<span data-ttu-id="9db61-211">100</span><span class="sxs-lookup"><span data-stu-id="9db61-211">100</span></span> |<span data-ttu-id="9db61-212">100</span><span class="sxs-lookup"><span data-stu-id="9db61-212">100</span></span> |<span data-ttu-id="9db61-213">200</span><span class="sxs-lookup"><span data-stu-id="9db61-213">200</span></span> |<span data-ttu-id="9db61-214">400</span><span class="sxs-lookup"><span data-stu-id="9db61-214">400</span></span> |
| <span data-ttu-id="9db61-215">DW200</span><span class="sxs-lookup"><span data-stu-id="9db61-215">DW200</span></span> |<span data-ttu-id="9db61-216">100</span><span class="sxs-lookup"><span data-stu-id="9db61-216">100</span></span> |<span data-ttu-id="9db61-217">200</span><span class="sxs-lookup"><span data-stu-id="9db61-217">200</span></span> |<span data-ttu-id="9db61-218">400</span><span class="sxs-lookup"><span data-stu-id="9db61-218">400</span></span> |<span data-ttu-id="9db61-219">800</span><span class="sxs-lookup"><span data-stu-id="9db61-219">800</span></span> |
| <span data-ttu-id="9db61-220">DW300</span><span class="sxs-lookup"><span data-stu-id="9db61-220">DW300</span></span> |<span data-ttu-id="9db61-221">100</span><span class="sxs-lookup"><span data-stu-id="9db61-221">100</span></span> |<span data-ttu-id="9db61-222">200</span><span class="sxs-lookup"><span data-stu-id="9db61-222">200</span></span> |<span data-ttu-id="9db61-223">400</span><span class="sxs-lookup"><span data-stu-id="9db61-223">400</span></span> |<span data-ttu-id="9db61-224">800</span><span class="sxs-lookup"><span data-stu-id="9db61-224">800</span></span> |
| <span data-ttu-id="9db61-225">DW400</span><span class="sxs-lookup"><span data-stu-id="9db61-225">DW400</span></span> |<span data-ttu-id="9db61-226">100</span><span class="sxs-lookup"><span data-stu-id="9db61-226">100</span></span> |<span data-ttu-id="9db61-227">400</span><span class="sxs-lookup"><span data-stu-id="9db61-227">400</span></span> |<span data-ttu-id="9db61-228">800</span><span class="sxs-lookup"><span data-stu-id="9db61-228">800</span></span> |<span data-ttu-id="9db61-229">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-229">1,600</span></span> |
| <span data-ttu-id="9db61-230">DW500</span><span class="sxs-lookup"><span data-stu-id="9db61-230">DW500</span></span> |<span data-ttu-id="9db61-231">100</span><span class="sxs-lookup"><span data-stu-id="9db61-231">100</span></span> |<span data-ttu-id="9db61-232">400</span><span class="sxs-lookup"><span data-stu-id="9db61-232">400</span></span> |<span data-ttu-id="9db61-233">800</span><span class="sxs-lookup"><span data-stu-id="9db61-233">800</span></span> |<span data-ttu-id="9db61-234">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-234">1,600</span></span> |
| <span data-ttu-id="9db61-235">DW600</span><span class="sxs-lookup"><span data-stu-id="9db61-235">DW600</span></span> |<span data-ttu-id="9db61-236">100</span><span class="sxs-lookup"><span data-stu-id="9db61-236">100</span></span> |<span data-ttu-id="9db61-237">400</span><span class="sxs-lookup"><span data-stu-id="9db61-237">400</span></span> |<span data-ttu-id="9db61-238">800</span><span class="sxs-lookup"><span data-stu-id="9db61-238">800</span></span> |<span data-ttu-id="9db61-239">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-239">1,600</span></span> |
| <span data-ttu-id="9db61-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="9db61-240">DW1000</span></span> |<span data-ttu-id="9db61-241">100</span><span class="sxs-lookup"><span data-stu-id="9db61-241">100</span></span> |<span data-ttu-id="9db61-242">800</span><span class="sxs-lookup"><span data-stu-id="9db61-242">800</span></span> |<span data-ttu-id="9db61-243">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-243">1,600</span></span> |<span data-ttu-id="9db61-244">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-244">3,200</span></span> |
| <span data-ttu-id="9db61-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="9db61-245">DW1200</span></span> |<span data-ttu-id="9db61-246">100</span><span class="sxs-lookup"><span data-stu-id="9db61-246">100</span></span> |<span data-ttu-id="9db61-247">800</span><span class="sxs-lookup"><span data-stu-id="9db61-247">800</span></span> |<span data-ttu-id="9db61-248">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-248">1,600</span></span> |<span data-ttu-id="9db61-249">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-249">3,200</span></span> |
| <span data-ttu-id="9db61-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="9db61-250">DW1500</span></span> |<span data-ttu-id="9db61-251">100</span><span class="sxs-lookup"><span data-stu-id="9db61-251">100</span></span> |<span data-ttu-id="9db61-252">800</span><span class="sxs-lookup"><span data-stu-id="9db61-252">800</span></span> |<span data-ttu-id="9db61-253">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-253">1,600</span></span> |<span data-ttu-id="9db61-254">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-254">3,200</span></span> |
| <span data-ttu-id="9db61-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="9db61-255">DW2000</span></span> |<span data-ttu-id="9db61-256">100</span><span class="sxs-lookup"><span data-stu-id="9db61-256">100</span></span> |<span data-ttu-id="9db61-257">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-257">1,600</span></span> |<span data-ttu-id="9db61-258">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-258">3,200</span></span> |<span data-ttu-id="9db61-259">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-259">6,400</span></span> |
| <span data-ttu-id="9db61-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="9db61-260">DW3000</span></span> |<span data-ttu-id="9db61-261">100</span><span class="sxs-lookup"><span data-stu-id="9db61-261">100</span></span> |<span data-ttu-id="9db61-262">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-262">1,600</span></span> |<span data-ttu-id="9db61-263">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-263">3,200</span></span> |<span data-ttu-id="9db61-264">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-264">6,400</span></span> |
| <span data-ttu-id="9db61-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="9db61-265">DW6000</span></span> |<span data-ttu-id="9db61-266">100</span><span class="sxs-lookup"><span data-stu-id="9db61-266">100</span></span> |<span data-ttu-id="9db61-267">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-267">3,200</span></span> |<span data-ttu-id="9db61-268">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-268">6,400</span></span> |<span data-ttu-id="9db61-269">12 800</span><span class="sxs-lookup"><span data-stu-id="9db61-269">12,800</span></span> |

<span data-ttu-id="9db61-270">в следующей таблице Hello сопоставляет hello память, выделенную распространения tooeach DWU и класс статический ресурс.</span><span class="sxs-lookup"><span data-stu-id="9db61-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="9db61-271">Обратите внимание, что классы более высокого ресурсов hello их память сокращение ограничения глобальных DWU toohonor hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="9db61-272">Выделение памяти на распределение для классов статических ресурсов (в МБ)</span><span class="sxs-lookup"><span data-stu-id="9db61-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="9db61-273">DWU</span><span class="sxs-lookup"><span data-stu-id="9db61-273">DWU</span></span> | <span data-ttu-id="9db61-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="9db61-274">staticrc10</span></span> | <span data-ttu-id="9db61-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="9db61-275">staticrc20</span></span> | <span data-ttu-id="9db61-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="9db61-276">staticrc30</span></span> | <span data-ttu-id="9db61-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="9db61-277">staticrc40</span></span> | <span data-ttu-id="9db61-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="9db61-278">staticrc50</span></span> | <span data-ttu-id="9db61-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="9db61-279">staticrc60</span></span> | <span data-ttu-id="9db61-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="9db61-280">staticrc70</span></span> | <span data-ttu-id="9db61-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="9db61-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9db61-282">DW100</span><span class="sxs-lookup"><span data-stu-id="9db61-282">DW100</span></span> |<span data-ttu-id="9db61-283">100</span><span class="sxs-lookup"><span data-stu-id="9db61-283">100</span></span> |<span data-ttu-id="9db61-284">200</span><span class="sxs-lookup"><span data-stu-id="9db61-284">200</span></span> |<span data-ttu-id="9db61-285">400</span><span class="sxs-lookup"><span data-stu-id="9db61-285">400</span></span> |<span data-ttu-id="9db61-286">400</span><span class="sxs-lookup"><span data-stu-id="9db61-286">400</span></span> |<span data-ttu-id="9db61-287">400</span><span class="sxs-lookup"><span data-stu-id="9db61-287">400</span></span> |<span data-ttu-id="9db61-288">400</span><span class="sxs-lookup"><span data-stu-id="9db61-288">400</span></span> |<span data-ttu-id="9db61-289">400</span><span class="sxs-lookup"><span data-stu-id="9db61-289">400</span></span> |<span data-ttu-id="9db61-290">400</span><span class="sxs-lookup"><span data-stu-id="9db61-290">400</span></span> |
| <span data-ttu-id="9db61-291">DW200</span><span class="sxs-lookup"><span data-stu-id="9db61-291">DW200</span></span> |<span data-ttu-id="9db61-292">100</span><span class="sxs-lookup"><span data-stu-id="9db61-292">100</span></span> |<span data-ttu-id="9db61-293">200</span><span class="sxs-lookup"><span data-stu-id="9db61-293">200</span></span> |<span data-ttu-id="9db61-294">400</span><span class="sxs-lookup"><span data-stu-id="9db61-294">400</span></span> |<span data-ttu-id="9db61-295">800</span><span class="sxs-lookup"><span data-stu-id="9db61-295">800</span></span> |<span data-ttu-id="9db61-296">800</span><span class="sxs-lookup"><span data-stu-id="9db61-296">800</span></span> |<span data-ttu-id="9db61-297">800</span><span class="sxs-lookup"><span data-stu-id="9db61-297">800</span></span> |<span data-ttu-id="9db61-298">800</span><span class="sxs-lookup"><span data-stu-id="9db61-298">800</span></span> |<span data-ttu-id="9db61-299">800</span><span class="sxs-lookup"><span data-stu-id="9db61-299">800</span></span> |
| <span data-ttu-id="9db61-300">DW300</span><span class="sxs-lookup"><span data-stu-id="9db61-300">DW300</span></span> |<span data-ttu-id="9db61-301">100</span><span class="sxs-lookup"><span data-stu-id="9db61-301">100</span></span> |<span data-ttu-id="9db61-302">200</span><span class="sxs-lookup"><span data-stu-id="9db61-302">200</span></span> |<span data-ttu-id="9db61-303">400</span><span class="sxs-lookup"><span data-stu-id="9db61-303">400</span></span> |<span data-ttu-id="9db61-304">800</span><span class="sxs-lookup"><span data-stu-id="9db61-304">800</span></span> |<span data-ttu-id="9db61-305">800</span><span class="sxs-lookup"><span data-stu-id="9db61-305">800</span></span> |<span data-ttu-id="9db61-306">800</span><span class="sxs-lookup"><span data-stu-id="9db61-306">800</span></span> |<span data-ttu-id="9db61-307">800</span><span class="sxs-lookup"><span data-stu-id="9db61-307">800</span></span> |<span data-ttu-id="9db61-308">800</span><span class="sxs-lookup"><span data-stu-id="9db61-308">800</span></span> |
| <span data-ttu-id="9db61-309">DW400</span><span class="sxs-lookup"><span data-stu-id="9db61-309">DW400</span></span> |<span data-ttu-id="9db61-310">100</span><span class="sxs-lookup"><span data-stu-id="9db61-310">100</span></span> |<span data-ttu-id="9db61-311">200</span><span class="sxs-lookup"><span data-stu-id="9db61-311">200</span></span> |<span data-ttu-id="9db61-312">400</span><span class="sxs-lookup"><span data-stu-id="9db61-312">400</span></span> |<span data-ttu-id="9db61-313">800</span><span class="sxs-lookup"><span data-stu-id="9db61-313">800</span></span> |<span data-ttu-id="9db61-314">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-314">1,600</span></span> |<span data-ttu-id="9db61-315">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-315">1,600</span></span> |<span data-ttu-id="9db61-316">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-316">1,600</span></span> |<span data-ttu-id="9db61-317">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-317">1,600</span></span> |
| <span data-ttu-id="9db61-318">DW500</span><span class="sxs-lookup"><span data-stu-id="9db61-318">DW500</span></span> |<span data-ttu-id="9db61-319">100</span><span class="sxs-lookup"><span data-stu-id="9db61-319">100</span></span> |<span data-ttu-id="9db61-320">200</span><span class="sxs-lookup"><span data-stu-id="9db61-320">200</span></span> |<span data-ttu-id="9db61-321">400</span><span class="sxs-lookup"><span data-stu-id="9db61-321">400</span></span> |<span data-ttu-id="9db61-322">800</span><span class="sxs-lookup"><span data-stu-id="9db61-322">800</span></span> |<span data-ttu-id="9db61-323">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-323">1,600</span></span> |<span data-ttu-id="9db61-324">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-324">1,600</span></span> |<span data-ttu-id="9db61-325">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-325">1,600</span></span> |<span data-ttu-id="9db61-326">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-326">1,600</span></span> |
| <span data-ttu-id="9db61-327">DW600</span><span class="sxs-lookup"><span data-stu-id="9db61-327">DW600</span></span> |<span data-ttu-id="9db61-328">100</span><span class="sxs-lookup"><span data-stu-id="9db61-328">100</span></span> |<span data-ttu-id="9db61-329">200</span><span class="sxs-lookup"><span data-stu-id="9db61-329">200</span></span> |<span data-ttu-id="9db61-330">400</span><span class="sxs-lookup"><span data-stu-id="9db61-330">400</span></span> |<span data-ttu-id="9db61-331">800</span><span class="sxs-lookup"><span data-stu-id="9db61-331">800</span></span> |<span data-ttu-id="9db61-332">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-332">1,600</span></span> |<span data-ttu-id="9db61-333">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-333">1,600</span></span> |<span data-ttu-id="9db61-334">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-334">1,600</span></span> |<span data-ttu-id="9db61-335">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-335">1,600</span></span> |
| <span data-ttu-id="9db61-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="9db61-336">DW1000</span></span> |<span data-ttu-id="9db61-337">100</span><span class="sxs-lookup"><span data-stu-id="9db61-337">100</span></span> |<span data-ttu-id="9db61-338">200</span><span class="sxs-lookup"><span data-stu-id="9db61-338">200</span></span> |<span data-ttu-id="9db61-339">400</span><span class="sxs-lookup"><span data-stu-id="9db61-339">400</span></span> |<span data-ttu-id="9db61-340">800</span><span class="sxs-lookup"><span data-stu-id="9db61-340">800</span></span> |<span data-ttu-id="9db61-341">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-341">1,600</span></span> |<span data-ttu-id="9db61-342">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-342">3,200</span></span> |<span data-ttu-id="9db61-343">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-343">3,200</span></span> |<span data-ttu-id="9db61-344">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-344">3,200</span></span> |
| <span data-ttu-id="9db61-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="9db61-345">DW1200</span></span> |<span data-ttu-id="9db61-346">100</span><span class="sxs-lookup"><span data-stu-id="9db61-346">100</span></span> |<span data-ttu-id="9db61-347">200</span><span class="sxs-lookup"><span data-stu-id="9db61-347">200</span></span> |<span data-ttu-id="9db61-348">400</span><span class="sxs-lookup"><span data-stu-id="9db61-348">400</span></span> |<span data-ttu-id="9db61-349">800</span><span class="sxs-lookup"><span data-stu-id="9db61-349">800</span></span> |<span data-ttu-id="9db61-350">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-350">1,600</span></span> |<span data-ttu-id="9db61-351">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-351">3,200</span></span> |<span data-ttu-id="9db61-352">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-352">3,200</span></span> |<span data-ttu-id="9db61-353">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-353">3,200</span></span> |
| <span data-ttu-id="9db61-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="9db61-354">DW1500</span></span> |<span data-ttu-id="9db61-355">100</span><span class="sxs-lookup"><span data-stu-id="9db61-355">100</span></span> |<span data-ttu-id="9db61-356">200</span><span class="sxs-lookup"><span data-stu-id="9db61-356">200</span></span> |<span data-ttu-id="9db61-357">400</span><span class="sxs-lookup"><span data-stu-id="9db61-357">400</span></span> |<span data-ttu-id="9db61-358">800</span><span class="sxs-lookup"><span data-stu-id="9db61-358">800</span></span> |<span data-ttu-id="9db61-359">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-359">1,600</span></span> |<span data-ttu-id="9db61-360">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-360">3,200</span></span> |<span data-ttu-id="9db61-361">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-361">3,200</span></span> |<span data-ttu-id="9db61-362">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-362">3,200</span></span> |
| <span data-ttu-id="9db61-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="9db61-363">DW2000</span></span> |<span data-ttu-id="9db61-364">100</span><span class="sxs-lookup"><span data-stu-id="9db61-364">100</span></span> |<span data-ttu-id="9db61-365">200</span><span class="sxs-lookup"><span data-stu-id="9db61-365">200</span></span> |<span data-ttu-id="9db61-366">400</span><span class="sxs-lookup"><span data-stu-id="9db61-366">400</span></span> |<span data-ttu-id="9db61-367">800</span><span class="sxs-lookup"><span data-stu-id="9db61-367">800</span></span> |<span data-ttu-id="9db61-368">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-368">1,600</span></span> |<span data-ttu-id="9db61-369">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-369">3,200</span></span> |<span data-ttu-id="9db61-370">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-370">6,400</span></span> |<span data-ttu-id="9db61-371">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-371">6,400</span></span> |
| <span data-ttu-id="9db61-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="9db61-372">DW3000</span></span> |<span data-ttu-id="9db61-373">100</span><span class="sxs-lookup"><span data-stu-id="9db61-373">100</span></span> |<span data-ttu-id="9db61-374">200</span><span class="sxs-lookup"><span data-stu-id="9db61-374">200</span></span> |<span data-ttu-id="9db61-375">400</span><span class="sxs-lookup"><span data-stu-id="9db61-375">400</span></span> |<span data-ttu-id="9db61-376">800</span><span class="sxs-lookup"><span data-stu-id="9db61-376">800</span></span> |<span data-ttu-id="9db61-377">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-377">1,600</span></span> |<span data-ttu-id="9db61-378">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-378">3,200</span></span> |<span data-ttu-id="9db61-379">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-379">6,400</span></span> |<span data-ttu-id="9db61-380">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-380">6,400</span></span> |
| <span data-ttu-id="9db61-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="9db61-381">DW6000</span></span> |<span data-ttu-id="9db61-382">100</span><span class="sxs-lookup"><span data-stu-id="9db61-382">100</span></span> |<span data-ttu-id="9db61-383">200</span><span class="sxs-lookup"><span data-stu-id="9db61-383">200</span></span> |<span data-ttu-id="9db61-384">400</span><span class="sxs-lookup"><span data-stu-id="9db61-384">400</span></span> |<span data-ttu-id="9db61-385">800</span><span class="sxs-lookup"><span data-stu-id="9db61-385">800</span></span> |<span data-ttu-id="9db61-386">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-386">1,600</span></span> |<span data-ttu-id="9db61-387">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-387">3,200</span></span> |<span data-ttu-id="9db61-388">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-388">6,400</span></span> |<span data-ttu-id="9db61-389">12 800</span><span class="sxs-lookup"><span data-stu-id="9db61-389">12,800</span></span> |

<span data-ttu-id="9db61-390">Из hello предшествующей таблице, можно видеть, что запрос на DW2000 в hello **xlargerc** класс ресурсов будет иметь доступ too6, 400 МБ памяти в пределах каждой hello 60 распределенных баз данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="9db61-391">В хранилище данных SQL используется 60 распределений.</span><span class="sxs-lookup"><span data-stu-id="9db61-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="9db61-392">Таким образом toocalculate hello общая память, выделенная для запроса в классе данного ресурса, hello выше значения необходимо будет умножено на 60.</span><span class="sxs-lookup"><span data-stu-id="9db61-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="9db61-393">Выделение памяти для всей системы (ГБ)</span><span class="sxs-lookup"><span data-stu-id="9db61-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="9db61-394">DWU</span><span class="sxs-lookup"><span data-stu-id="9db61-394">DWU</span></span> | <span data-ttu-id="9db61-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="9db61-395">smallrc</span></span> | <span data-ttu-id="9db61-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="9db61-396">mediumrc</span></span> | <span data-ttu-id="9db61-397">largerc</span><span class="sxs-lookup"><span data-stu-id="9db61-397">largerc</span></span> | <span data-ttu-id="9db61-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="9db61-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="9db61-399">DW100</span><span class="sxs-lookup"><span data-stu-id="9db61-399">DW100</span></span> |<span data-ttu-id="9db61-400">6</span><span class="sxs-lookup"><span data-stu-id="9db61-400">6</span></span> |<span data-ttu-id="9db61-401">6</span><span class="sxs-lookup"><span data-stu-id="9db61-401">6</span></span> |<span data-ttu-id="9db61-402">12</span><span class="sxs-lookup"><span data-stu-id="9db61-402">12</span></span> |<span data-ttu-id="9db61-403">23</span><span class="sxs-lookup"><span data-stu-id="9db61-403">23</span></span> |
| <span data-ttu-id="9db61-404">DW200</span><span class="sxs-lookup"><span data-stu-id="9db61-404">DW200</span></span> |<span data-ttu-id="9db61-405">6</span><span class="sxs-lookup"><span data-stu-id="9db61-405">6</span></span> |<span data-ttu-id="9db61-406">12</span><span class="sxs-lookup"><span data-stu-id="9db61-406">12</span></span> |<span data-ttu-id="9db61-407">23</span><span class="sxs-lookup"><span data-stu-id="9db61-407">23</span></span> |<span data-ttu-id="9db61-408">47</span><span class="sxs-lookup"><span data-stu-id="9db61-408">47</span></span> |
| <span data-ttu-id="9db61-409">DW300</span><span class="sxs-lookup"><span data-stu-id="9db61-409">DW300</span></span> |<span data-ttu-id="9db61-410">6</span><span class="sxs-lookup"><span data-stu-id="9db61-410">6</span></span> |<span data-ttu-id="9db61-411">12</span><span class="sxs-lookup"><span data-stu-id="9db61-411">12</span></span> |<span data-ttu-id="9db61-412">23</span><span class="sxs-lookup"><span data-stu-id="9db61-412">23</span></span> |<span data-ttu-id="9db61-413">47</span><span class="sxs-lookup"><span data-stu-id="9db61-413">47</span></span> |
| <span data-ttu-id="9db61-414">DW400</span><span class="sxs-lookup"><span data-stu-id="9db61-414">DW400</span></span> |<span data-ttu-id="9db61-415">6</span><span class="sxs-lookup"><span data-stu-id="9db61-415">6</span></span> |<span data-ttu-id="9db61-416">23</span><span class="sxs-lookup"><span data-stu-id="9db61-416">23</span></span> |<span data-ttu-id="9db61-417">47</span><span class="sxs-lookup"><span data-stu-id="9db61-417">47</span></span> |<span data-ttu-id="9db61-418">94</span><span class="sxs-lookup"><span data-stu-id="9db61-418">94</span></span> |
| <span data-ttu-id="9db61-419">DW500</span><span class="sxs-lookup"><span data-stu-id="9db61-419">DW500</span></span> |<span data-ttu-id="9db61-420">6</span><span class="sxs-lookup"><span data-stu-id="9db61-420">6</span></span> |<span data-ttu-id="9db61-421">23</span><span class="sxs-lookup"><span data-stu-id="9db61-421">23</span></span> |<span data-ttu-id="9db61-422">47</span><span class="sxs-lookup"><span data-stu-id="9db61-422">47</span></span> |<span data-ttu-id="9db61-423">94</span><span class="sxs-lookup"><span data-stu-id="9db61-423">94</span></span> |
| <span data-ttu-id="9db61-424">DW600</span><span class="sxs-lookup"><span data-stu-id="9db61-424">DW600</span></span> |<span data-ttu-id="9db61-425">6</span><span class="sxs-lookup"><span data-stu-id="9db61-425">6</span></span> |<span data-ttu-id="9db61-426">23</span><span class="sxs-lookup"><span data-stu-id="9db61-426">23</span></span> |<span data-ttu-id="9db61-427">47</span><span class="sxs-lookup"><span data-stu-id="9db61-427">47</span></span> |<span data-ttu-id="9db61-428">94</span><span class="sxs-lookup"><span data-stu-id="9db61-428">94</span></span> |
| <span data-ttu-id="9db61-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="9db61-429">DW1000</span></span> |<span data-ttu-id="9db61-430">6</span><span class="sxs-lookup"><span data-stu-id="9db61-430">6</span></span> |<span data-ttu-id="9db61-431">47</span><span class="sxs-lookup"><span data-stu-id="9db61-431">47</span></span> |<span data-ttu-id="9db61-432">94</span><span class="sxs-lookup"><span data-stu-id="9db61-432">94</span></span> |<span data-ttu-id="9db61-433">188</span><span class="sxs-lookup"><span data-stu-id="9db61-433">188</span></span> |
| <span data-ttu-id="9db61-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="9db61-434">DW1200</span></span> |<span data-ttu-id="9db61-435">6</span><span class="sxs-lookup"><span data-stu-id="9db61-435">6</span></span> |<span data-ttu-id="9db61-436">47</span><span class="sxs-lookup"><span data-stu-id="9db61-436">47</span></span> |<span data-ttu-id="9db61-437">94</span><span class="sxs-lookup"><span data-stu-id="9db61-437">94</span></span> |<span data-ttu-id="9db61-438">188</span><span class="sxs-lookup"><span data-stu-id="9db61-438">188</span></span> |
| <span data-ttu-id="9db61-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="9db61-439">DW1500</span></span> |<span data-ttu-id="9db61-440">6</span><span class="sxs-lookup"><span data-stu-id="9db61-440">6</span></span> |<span data-ttu-id="9db61-441">47</span><span class="sxs-lookup"><span data-stu-id="9db61-441">47</span></span> |<span data-ttu-id="9db61-442">94</span><span class="sxs-lookup"><span data-stu-id="9db61-442">94</span></span> |<span data-ttu-id="9db61-443">188</span><span class="sxs-lookup"><span data-stu-id="9db61-443">188</span></span> |
| <span data-ttu-id="9db61-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="9db61-444">DW2000</span></span> |<span data-ttu-id="9db61-445">6</span><span class="sxs-lookup"><span data-stu-id="9db61-445">6</span></span> |<span data-ttu-id="9db61-446">94</span><span class="sxs-lookup"><span data-stu-id="9db61-446">94</span></span> |<span data-ttu-id="9db61-447">188</span><span class="sxs-lookup"><span data-stu-id="9db61-447">188</span></span> |<span data-ttu-id="9db61-448">375</span><span class="sxs-lookup"><span data-stu-id="9db61-448">375</span></span> |
| <span data-ttu-id="9db61-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="9db61-449">DW3000</span></span> |<span data-ttu-id="9db61-450">6</span><span class="sxs-lookup"><span data-stu-id="9db61-450">6</span></span> |<span data-ttu-id="9db61-451">94</span><span class="sxs-lookup"><span data-stu-id="9db61-451">94</span></span> |<span data-ttu-id="9db61-452">188</span><span class="sxs-lookup"><span data-stu-id="9db61-452">188</span></span> |<span data-ttu-id="9db61-453">375</span><span class="sxs-lookup"><span data-stu-id="9db61-453">375</span></span> |
| <span data-ttu-id="9db61-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="9db61-454">DW6000</span></span> |<span data-ttu-id="9db61-455">6</span><span class="sxs-lookup"><span data-stu-id="9db61-455">6</span></span> |<span data-ttu-id="9db61-456">188</span><span class="sxs-lookup"><span data-stu-id="9db61-456">188</span></span> |<span data-ttu-id="9db61-457">375</span><span class="sxs-lookup"><span data-stu-id="9db61-457">375</span></span> |<span data-ttu-id="9db61-458">750</span><span class="sxs-lookup"><span data-stu-id="9db61-458">750</span></span> |

<span data-ttu-id="9db61-459">Из этой таблицы распределения памяти во всей системе, можно увидеть, что запрос на DW2000 в классе ресурса xlargerc hello выделена общий 375 ГБ памяти (распределения 6 400 МБ * 60 / 1024 tooconvert tooGB) на время всего hello хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9db61-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="9db61-460">Hello же применяется вычисление классов toostatic ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="9db61-461">Использование слотов выдачи</span><span class="sxs-lookup"><span data-stu-id="9db61-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="9db61-462">Хранилище данных SQL предоставляет дополнительные tooqueries памяти, работающих в более высоких классов ресурса.</span><span class="sxs-lookup"><span data-stu-id="9db61-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="9db61-463">Память — фиксированный ресурс.</span><span class="sxs-lookup"><span data-stu-id="9db61-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="9db61-464">Таким образом hello выделена дополнительная память каждого запроса, hello, которые можно выполнять меньшее число параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="9db61-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="9db61-465">Hello следующей таблице reiterates все предыдущие принципы hello в одном представлении, показывающая количество hello параллелизма слоты, имеющиеся по DWU и слоты hello, потребляемых каждого класса ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="9db61-466">Выделение и использование слотов параллельности для классов динамических ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="9db61-467">DWU</span><span class="sxs-lookup"><span data-stu-id="9db61-467">DWU</span></span> | <span data-ttu-id="9db61-468">Максимальное число одновременных запросов</span><span class="sxs-lookup"><span data-stu-id="9db61-468">Maximum concurrent queries</span></span> | <span data-ttu-id="9db61-469">Число выделенных слотов выдачи</span><span class="sxs-lookup"><span data-stu-id="9db61-469">Concurrency slots allocated</span></span> | <span data-ttu-id="9db61-470">Слоты, используемые smallrc</span><span class="sxs-lookup"><span data-stu-id="9db61-470">Slots used by smallrc</span></span> | <span data-ttu-id="9db61-471">Слоты, используемые mediumrc</span><span class="sxs-lookup"><span data-stu-id="9db61-471">Slots used by mediumrc</span></span> | <span data-ttu-id="9db61-472">Слоты, используемые largerc</span><span class="sxs-lookup"><span data-stu-id="9db61-472">Slots used by largerc</span></span> | <span data-ttu-id="9db61-473">Слоты, используемые xlargerc</span><span class="sxs-lookup"><span data-stu-id="9db61-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9db61-474">DW100</span><span class="sxs-lookup"><span data-stu-id="9db61-474">DW100</span></span> |<span data-ttu-id="9db61-475">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-475">4</span></span> |<span data-ttu-id="9db61-476">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-476">4</span></span> |<span data-ttu-id="9db61-477">1</span><span class="sxs-lookup"><span data-stu-id="9db61-477">1</span></span> |<span data-ttu-id="9db61-478">1</span><span class="sxs-lookup"><span data-stu-id="9db61-478">1</span></span> |<span data-ttu-id="9db61-479">2</span><span class="sxs-lookup"><span data-stu-id="9db61-479">2</span></span> |<span data-ttu-id="9db61-480">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-480">4</span></span> |
| <span data-ttu-id="9db61-481">DW200</span><span class="sxs-lookup"><span data-stu-id="9db61-481">DW200</span></span> |<span data-ttu-id="9db61-482">8</span><span class="sxs-lookup"><span data-stu-id="9db61-482">8</span></span> |<span data-ttu-id="9db61-483">8</span><span class="sxs-lookup"><span data-stu-id="9db61-483">8</span></span> |<span data-ttu-id="9db61-484">1</span><span class="sxs-lookup"><span data-stu-id="9db61-484">1</span></span> |<span data-ttu-id="9db61-485">2</span><span class="sxs-lookup"><span data-stu-id="9db61-485">2</span></span> |<span data-ttu-id="9db61-486">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-486">4</span></span> |<span data-ttu-id="9db61-487">8</span><span class="sxs-lookup"><span data-stu-id="9db61-487">8</span></span> |
| <span data-ttu-id="9db61-488">DW300</span><span class="sxs-lookup"><span data-stu-id="9db61-488">DW300</span></span> |<span data-ttu-id="9db61-489">12</span><span class="sxs-lookup"><span data-stu-id="9db61-489">12</span></span> |<span data-ttu-id="9db61-490">12</span><span class="sxs-lookup"><span data-stu-id="9db61-490">12</span></span> |<span data-ttu-id="9db61-491">1</span><span class="sxs-lookup"><span data-stu-id="9db61-491">1</span></span> |<span data-ttu-id="9db61-492">2</span><span class="sxs-lookup"><span data-stu-id="9db61-492">2</span></span> |<span data-ttu-id="9db61-493">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-493">4</span></span> |<span data-ttu-id="9db61-494">8</span><span class="sxs-lookup"><span data-stu-id="9db61-494">8</span></span> |
| <span data-ttu-id="9db61-495">DW400</span><span class="sxs-lookup"><span data-stu-id="9db61-495">DW400</span></span> |<span data-ttu-id="9db61-496">16</span><span class="sxs-lookup"><span data-stu-id="9db61-496">16</span></span> |<span data-ttu-id="9db61-497">16</span><span class="sxs-lookup"><span data-stu-id="9db61-497">16</span></span> |<span data-ttu-id="9db61-498">1</span><span class="sxs-lookup"><span data-stu-id="9db61-498">1</span></span> |<span data-ttu-id="9db61-499">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-499">4</span></span> |<span data-ttu-id="9db61-500">8</span><span class="sxs-lookup"><span data-stu-id="9db61-500">8</span></span> |<span data-ttu-id="9db61-501">16</span><span class="sxs-lookup"><span data-stu-id="9db61-501">16</span></span> |
| <span data-ttu-id="9db61-502">DW500</span><span class="sxs-lookup"><span data-stu-id="9db61-502">DW500</span></span> |<span data-ttu-id="9db61-503">20</span><span class="sxs-lookup"><span data-stu-id="9db61-503">20</span></span> |<span data-ttu-id="9db61-504">20</span><span class="sxs-lookup"><span data-stu-id="9db61-504">20</span></span> |<span data-ttu-id="9db61-505">1</span><span class="sxs-lookup"><span data-stu-id="9db61-505">1</span></span> |<span data-ttu-id="9db61-506">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-506">4</span></span> |<span data-ttu-id="9db61-507">8</span><span class="sxs-lookup"><span data-stu-id="9db61-507">8</span></span> |<span data-ttu-id="9db61-508">16</span><span class="sxs-lookup"><span data-stu-id="9db61-508">16</span></span> |
| <span data-ttu-id="9db61-509">DW600</span><span class="sxs-lookup"><span data-stu-id="9db61-509">DW600</span></span> |<span data-ttu-id="9db61-510">24</span><span class="sxs-lookup"><span data-stu-id="9db61-510">24</span></span> |<span data-ttu-id="9db61-511">24</span><span class="sxs-lookup"><span data-stu-id="9db61-511">24</span></span> |<span data-ttu-id="9db61-512">1</span><span class="sxs-lookup"><span data-stu-id="9db61-512">1</span></span> |<span data-ttu-id="9db61-513">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-513">4</span></span> |<span data-ttu-id="9db61-514">8</span><span class="sxs-lookup"><span data-stu-id="9db61-514">8</span></span> |<span data-ttu-id="9db61-515">16</span><span class="sxs-lookup"><span data-stu-id="9db61-515">16</span></span> |
| <span data-ttu-id="9db61-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="9db61-516">DW1000</span></span> |<span data-ttu-id="9db61-517">32</span><span class="sxs-lookup"><span data-stu-id="9db61-517">32</span></span> |<span data-ttu-id="9db61-518">40</span><span class="sxs-lookup"><span data-stu-id="9db61-518">40</span></span> |<span data-ttu-id="9db61-519">1</span><span class="sxs-lookup"><span data-stu-id="9db61-519">1</span></span> |<span data-ttu-id="9db61-520">8</span><span class="sxs-lookup"><span data-stu-id="9db61-520">8</span></span> |<span data-ttu-id="9db61-521">16</span><span class="sxs-lookup"><span data-stu-id="9db61-521">16</span></span> |<span data-ttu-id="9db61-522">32</span><span class="sxs-lookup"><span data-stu-id="9db61-522">32</span></span> |
| <span data-ttu-id="9db61-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="9db61-523">DW1200</span></span> |<span data-ttu-id="9db61-524">32</span><span class="sxs-lookup"><span data-stu-id="9db61-524">32</span></span> |<span data-ttu-id="9db61-525">48</span><span class="sxs-lookup"><span data-stu-id="9db61-525">48</span></span> |<span data-ttu-id="9db61-526">1</span><span class="sxs-lookup"><span data-stu-id="9db61-526">1</span></span> |<span data-ttu-id="9db61-527">8</span><span class="sxs-lookup"><span data-stu-id="9db61-527">8</span></span> |<span data-ttu-id="9db61-528">16</span><span class="sxs-lookup"><span data-stu-id="9db61-528">16</span></span> |<span data-ttu-id="9db61-529">32</span><span class="sxs-lookup"><span data-stu-id="9db61-529">32</span></span> |
| <span data-ttu-id="9db61-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="9db61-530">DW1500</span></span> |<span data-ttu-id="9db61-531">32</span><span class="sxs-lookup"><span data-stu-id="9db61-531">32</span></span> |<span data-ttu-id="9db61-532">60</span><span class="sxs-lookup"><span data-stu-id="9db61-532">60</span></span> |<span data-ttu-id="9db61-533">1</span><span class="sxs-lookup"><span data-stu-id="9db61-533">1</span></span> |<span data-ttu-id="9db61-534">8</span><span class="sxs-lookup"><span data-stu-id="9db61-534">8</span></span> |<span data-ttu-id="9db61-535">16</span><span class="sxs-lookup"><span data-stu-id="9db61-535">16</span></span> |<span data-ttu-id="9db61-536">32</span><span class="sxs-lookup"><span data-stu-id="9db61-536">32</span></span> |
| <span data-ttu-id="9db61-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="9db61-537">DW2000</span></span> |<span data-ttu-id="9db61-538">32</span><span class="sxs-lookup"><span data-stu-id="9db61-538">32</span></span> |<span data-ttu-id="9db61-539">80</span><span class="sxs-lookup"><span data-stu-id="9db61-539">80</span></span> |<span data-ttu-id="9db61-540">1</span><span class="sxs-lookup"><span data-stu-id="9db61-540">1</span></span> |<span data-ttu-id="9db61-541">16</span><span class="sxs-lookup"><span data-stu-id="9db61-541">16</span></span> |<span data-ttu-id="9db61-542">32</span><span class="sxs-lookup"><span data-stu-id="9db61-542">32</span></span> |<span data-ttu-id="9db61-543">64</span><span class="sxs-lookup"><span data-stu-id="9db61-543">64</span></span> |
| <span data-ttu-id="9db61-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="9db61-544">DW3000</span></span> |<span data-ttu-id="9db61-545">32</span><span class="sxs-lookup"><span data-stu-id="9db61-545">32</span></span> |<span data-ttu-id="9db61-546">120</span><span class="sxs-lookup"><span data-stu-id="9db61-546">120</span></span> |<span data-ttu-id="9db61-547">1</span><span class="sxs-lookup"><span data-stu-id="9db61-547">1</span></span> |<span data-ttu-id="9db61-548">16</span><span class="sxs-lookup"><span data-stu-id="9db61-548">16</span></span> |<span data-ttu-id="9db61-549">32</span><span class="sxs-lookup"><span data-stu-id="9db61-549">32</span></span> |<span data-ttu-id="9db61-550">64</span><span class="sxs-lookup"><span data-stu-id="9db61-550">64</span></span> |
| <span data-ttu-id="9db61-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="9db61-551">DW6000</span></span> |<span data-ttu-id="9db61-552">32</span><span class="sxs-lookup"><span data-stu-id="9db61-552">32</span></span> |<span data-ttu-id="9db61-553">240</span><span class="sxs-lookup"><span data-stu-id="9db61-553">240</span></span> |<span data-ttu-id="9db61-554">1</span><span class="sxs-lookup"><span data-stu-id="9db61-554">1</span></span> |<span data-ttu-id="9db61-555">32</span><span class="sxs-lookup"><span data-stu-id="9db61-555">32</span></span> |<span data-ttu-id="9db61-556">64</span><span class="sxs-lookup"><span data-stu-id="9db61-556">64</span></span> |<span data-ttu-id="9db61-557">128</span><span class="sxs-lookup"><span data-stu-id="9db61-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="9db61-558">Выделение и использование слотов выдачи для классов статических ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="9db61-559">DWU</span><span class="sxs-lookup"><span data-stu-id="9db61-559">DWU</span></span> | <span data-ttu-id="9db61-560">Максимальное число одновременных запросов</span><span class="sxs-lookup"><span data-stu-id="9db61-560">Maximum concurrent queries</span></span> | <span data-ttu-id="9db61-561">Число выделенных слотов выдачи</span><span class="sxs-lookup"><span data-stu-id="9db61-561">Concurrency slots allocated</span></span> |<span data-ttu-id="9db61-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="9db61-562">staticrc10</span></span> | <span data-ttu-id="9db61-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="9db61-563">staticrc20</span></span> | <span data-ttu-id="9db61-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="9db61-564">staticrc30</span></span> | <span data-ttu-id="9db61-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="9db61-565">staticrc40</span></span> | <span data-ttu-id="9db61-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="9db61-566">staticrc50</span></span> | <span data-ttu-id="9db61-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="9db61-567">staticrc60</span></span> | <span data-ttu-id="9db61-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="9db61-568">staticrc70</span></span> | <span data-ttu-id="9db61-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="9db61-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9db61-570">DW100</span><span class="sxs-lookup"><span data-stu-id="9db61-570">DW100</span></span> |<span data-ttu-id="9db61-571">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-571">4</span></span> |<span data-ttu-id="9db61-572">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-572">4</span></span> |<span data-ttu-id="9db61-573">1</span><span class="sxs-lookup"><span data-stu-id="9db61-573">1</span></span> |<span data-ttu-id="9db61-574">2</span><span class="sxs-lookup"><span data-stu-id="9db61-574">2</span></span> |<span data-ttu-id="9db61-575">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-575">4</span></span> |<span data-ttu-id="9db61-576">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-576">4</span></span> |<span data-ttu-id="9db61-577">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-577">4</span></span> |<span data-ttu-id="9db61-578">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-578">4</span></span> |<span data-ttu-id="9db61-579">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-579">4</span></span> |<span data-ttu-id="9db61-580">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-580">4</span></span> |
| <span data-ttu-id="9db61-581">DW200</span><span class="sxs-lookup"><span data-stu-id="9db61-581">DW200</span></span> |<span data-ttu-id="9db61-582">8</span><span class="sxs-lookup"><span data-stu-id="9db61-582">8</span></span> |<span data-ttu-id="9db61-583">8</span><span class="sxs-lookup"><span data-stu-id="9db61-583">8</span></span> |<span data-ttu-id="9db61-584">1</span><span class="sxs-lookup"><span data-stu-id="9db61-584">1</span></span> |<span data-ttu-id="9db61-585">2</span><span class="sxs-lookup"><span data-stu-id="9db61-585">2</span></span> |<span data-ttu-id="9db61-586">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-586">4</span></span> |<span data-ttu-id="9db61-587">8</span><span class="sxs-lookup"><span data-stu-id="9db61-587">8</span></span> |<span data-ttu-id="9db61-588">8</span><span class="sxs-lookup"><span data-stu-id="9db61-588">8</span></span> |<span data-ttu-id="9db61-589">8</span><span class="sxs-lookup"><span data-stu-id="9db61-589">8</span></span> |<span data-ttu-id="9db61-590">8</span><span class="sxs-lookup"><span data-stu-id="9db61-590">8</span></span> |<span data-ttu-id="9db61-591">8</span><span class="sxs-lookup"><span data-stu-id="9db61-591">8</span></span> |
| <span data-ttu-id="9db61-592">DW300</span><span class="sxs-lookup"><span data-stu-id="9db61-592">DW300</span></span> |<span data-ttu-id="9db61-593">12</span><span class="sxs-lookup"><span data-stu-id="9db61-593">12</span></span> |<span data-ttu-id="9db61-594">12</span><span class="sxs-lookup"><span data-stu-id="9db61-594">12</span></span> |<span data-ttu-id="9db61-595">1</span><span class="sxs-lookup"><span data-stu-id="9db61-595">1</span></span> |<span data-ttu-id="9db61-596">2</span><span class="sxs-lookup"><span data-stu-id="9db61-596">2</span></span> |<span data-ttu-id="9db61-597">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-597">4</span></span> |<span data-ttu-id="9db61-598">8</span><span class="sxs-lookup"><span data-stu-id="9db61-598">8</span></span> |<span data-ttu-id="9db61-599">8</span><span class="sxs-lookup"><span data-stu-id="9db61-599">8</span></span> |<span data-ttu-id="9db61-600">8</span><span class="sxs-lookup"><span data-stu-id="9db61-600">8</span></span> |<span data-ttu-id="9db61-601">8</span><span class="sxs-lookup"><span data-stu-id="9db61-601">8</span></span> |<span data-ttu-id="9db61-602">8</span><span class="sxs-lookup"><span data-stu-id="9db61-602">8</span></span> |
| <span data-ttu-id="9db61-603">DW400</span><span class="sxs-lookup"><span data-stu-id="9db61-603">DW400</span></span> |<span data-ttu-id="9db61-604">16</span><span class="sxs-lookup"><span data-stu-id="9db61-604">16</span></span> |<span data-ttu-id="9db61-605">16</span><span class="sxs-lookup"><span data-stu-id="9db61-605">16</span></span> |<span data-ttu-id="9db61-606">1</span><span class="sxs-lookup"><span data-stu-id="9db61-606">1</span></span> |<span data-ttu-id="9db61-607">2</span><span class="sxs-lookup"><span data-stu-id="9db61-607">2</span></span> |<span data-ttu-id="9db61-608">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-608">4</span></span> |<span data-ttu-id="9db61-609">8</span><span class="sxs-lookup"><span data-stu-id="9db61-609">8</span></span> |<span data-ttu-id="9db61-610">16</span><span class="sxs-lookup"><span data-stu-id="9db61-610">16</span></span> |<span data-ttu-id="9db61-611">16</span><span class="sxs-lookup"><span data-stu-id="9db61-611">16</span></span> |<span data-ttu-id="9db61-612">16</span><span class="sxs-lookup"><span data-stu-id="9db61-612">16</span></span> |<span data-ttu-id="9db61-613">16</span><span class="sxs-lookup"><span data-stu-id="9db61-613">16</span></span> |
| <span data-ttu-id="9db61-614">DW500</span><span class="sxs-lookup"><span data-stu-id="9db61-614">DW500</span></span> | <span data-ttu-id="9db61-615">20</span><span class="sxs-lookup"><span data-stu-id="9db61-615">20</span></span>| <span data-ttu-id="9db61-616">20</span><span class="sxs-lookup"><span data-stu-id="9db61-616">20</span></span>| <span data-ttu-id="9db61-617">1</span><span class="sxs-lookup"><span data-stu-id="9db61-617">1</span></span>| <span data-ttu-id="9db61-618">2</span><span class="sxs-lookup"><span data-stu-id="9db61-618">2</span></span>| <span data-ttu-id="9db61-619">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-619">4</span></span>| <span data-ttu-id="9db61-620">8</span><span class="sxs-lookup"><span data-stu-id="9db61-620">8</span></span>| <span data-ttu-id="9db61-621">16</span><span class="sxs-lookup"><span data-stu-id="9db61-621">16</span></span>| <span data-ttu-id="9db61-622">16</span><span class="sxs-lookup"><span data-stu-id="9db61-622">16</span></span>| <span data-ttu-id="9db61-623">16</span><span class="sxs-lookup"><span data-stu-id="9db61-623">16</span></span>| <span data-ttu-id="9db61-624">16</span><span class="sxs-lookup"><span data-stu-id="9db61-624">16</span></span>|
| <span data-ttu-id="9db61-625">DW600</span><span class="sxs-lookup"><span data-stu-id="9db61-625">DW600</span></span> | <span data-ttu-id="9db61-626">24</span><span class="sxs-lookup"><span data-stu-id="9db61-626">24</span></span>| <span data-ttu-id="9db61-627">24</span><span class="sxs-lookup"><span data-stu-id="9db61-627">24</span></span>| <span data-ttu-id="9db61-628">1</span><span class="sxs-lookup"><span data-stu-id="9db61-628">1</span></span>| <span data-ttu-id="9db61-629">2</span><span class="sxs-lookup"><span data-stu-id="9db61-629">2</span></span>| <span data-ttu-id="9db61-630">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-630">4</span></span>| <span data-ttu-id="9db61-631">8</span><span class="sxs-lookup"><span data-stu-id="9db61-631">8</span></span>| <span data-ttu-id="9db61-632">16</span><span class="sxs-lookup"><span data-stu-id="9db61-632">16</span></span>| <span data-ttu-id="9db61-633">16</span><span class="sxs-lookup"><span data-stu-id="9db61-633">16</span></span>| <span data-ttu-id="9db61-634">16</span><span class="sxs-lookup"><span data-stu-id="9db61-634">16</span></span>| <span data-ttu-id="9db61-635">16</span><span class="sxs-lookup"><span data-stu-id="9db61-635">16</span></span>|
| <span data-ttu-id="9db61-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="9db61-636">DW1000</span></span> | <span data-ttu-id="9db61-637">32</span><span class="sxs-lookup"><span data-stu-id="9db61-637">32</span></span>| <span data-ttu-id="9db61-638">40</span><span class="sxs-lookup"><span data-stu-id="9db61-638">40</span></span>| <span data-ttu-id="9db61-639">1</span><span class="sxs-lookup"><span data-stu-id="9db61-639">1</span></span>| <span data-ttu-id="9db61-640">2</span><span class="sxs-lookup"><span data-stu-id="9db61-640">2</span></span>| <span data-ttu-id="9db61-641">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-641">4</span></span>| <span data-ttu-id="9db61-642">8</span><span class="sxs-lookup"><span data-stu-id="9db61-642">8</span></span>| <span data-ttu-id="9db61-643">16</span><span class="sxs-lookup"><span data-stu-id="9db61-643">16</span></span>| <span data-ttu-id="9db61-644">32</span><span class="sxs-lookup"><span data-stu-id="9db61-644">32</span></span>| <span data-ttu-id="9db61-645">32</span><span class="sxs-lookup"><span data-stu-id="9db61-645">32</span></span>| <span data-ttu-id="9db61-646">32</span><span class="sxs-lookup"><span data-stu-id="9db61-646">32</span></span>|
| <span data-ttu-id="9db61-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="9db61-647">DW1200</span></span> | <span data-ttu-id="9db61-648">32</span><span class="sxs-lookup"><span data-stu-id="9db61-648">32</span></span>| <span data-ttu-id="9db61-649">48</span><span class="sxs-lookup"><span data-stu-id="9db61-649">48</span></span>| <span data-ttu-id="9db61-650">1</span><span class="sxs-lookup"><span data-stu-id="9db61-650">1</span></span>| <span data-ttu-id="9db61-651">2</span><span class="sxs-lookup"><span data-stu-id="9db61-651">2</span></span>| <span data-ttu-id="9db61-652">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-652">4</span></span>| <span data-ttu-id="9db61-653">8</span><span class="sxs-lookup"><span data-stu-id="9db61-653">8</span></span>| <span data-ttu-id="9db61-654">16</span><span class="sxs-lookup"><span data-stu-id="9db61-654">16</span></span>| <span data-ttu-id="9db61-655">32</span><span class="sxs-lookup"><span data-stu-id="9db61-655">32</span></span>| <span data-ttu-id="9db61-656">32</span><span class="sxs-lookup"><span data-stu-id="9db61-656">32</span></span>| <span data-ttu-id="9db61-657">32</span><span class="sxs-lookup"><span data-stu-id="9db61-657">32</span></span>|
| <span data-ttu-id="9db61-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="9db61-658">DW1500</span></span> | <span data-ttu-id="9db61-659">32</span><span class="sxs-lookup"><span data-stu-id="9db61-659">32</span></span>| <span data-ttu-id="9db61-660">60</span><span class="sxs-lookup"><span data-stu-id="9db61-660">60</span></span>| <span data-ttu-id="9db61-661">1</span><span class="sxs-lookup"><span data-stu-id="9db61-661">1</span></span>| <span data-ttu-id="9db61-662">2</span><span class="sxs-lookup"><span data-stu-id="9db61-662">2</span></span>| <span data-ttu-id="9db61-663">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-663">4</span></span>| <span data-ttu-id="9db61-664">8</span><span class="sxs-lookup"><span data-stu-id="9db61-664">8</span></span>| <span data-ttu-id="9db61-665">16</span><span class="sxs-lookup"><span data-stu-id="9db61-665">16</span></span>| <span data-ttu-id="9db61-666">32</span><span class="sxs-lookup"><span data-stu-id="9db61-666">32</span></span>| <span data-ttu-id="9db61-667">32</span><span class="sxs-lookup"><span data-stu-id="9db61-667">32</span></span>| <span data-ttu-id="9db61-668">32</span><span class="sxs-lookup"><span data-stu-id="9db61-668">32</span></span>|
| <span data-ttu-id="9db61-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="9db61-669">DW2000</span></span> | <span data-ttu-id="9db61-670">32</span><span class="sxs-lookup"><span data-stu-id="9db61-670">32</span></span>| <span data-ttu-id="9db61-671">80</span><span class="sxs-lookup"><span data-stu-id="9db61-671">80</span></span>| <span data-ttu-id="9db61-672">1</span><span class="sxs-lookup"><span data-stu-id="9db61-672">1</span></span>| <span data-ttu-id="9db61-673">2</span><span class="sxs-lookup"><span data-stu-id="9db61-673">2</span></span>| <span data-ttu-id="9db61-674">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-674">4</span></span>| <span data-ttu-id="9db61-675">8</span><span class="sxs-lookup"><span data-stu-id="9db61-675">8</span></span>| <span data-ttu-id="9db61-676">16</span><span class="sxs-lookup"><span data-stu-id="9db61-676">16</span></span>| <span data-ttu-id="9db61-677">32</span><span class="sxs-lookup"><span data-stu-id="9db61-677">32</span></span>| <span data-ttu-id="9db61-678">64</span><span class="sxs-lookup"><span data-stu-id="9db61-678">64</span></span>| <span data-ttu-id="9db61-679">64</span><span class="sxs-lookup"><span data-stu-id="9db61-679">64</span></span>|
| <span data-ttu-id="9db61-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="9db61-680">DW3000</span></span> | <span data-ttu-id="9db61-681">32</span><span class="sxs-lookup"><span data-stu-id="9db61-681">32</span></span>| <span data-ttu-id="9db61-682">120</span><span class="sxs-lookup"><span data-stu-id="9db61-682">120</span></span>| <span data-ttu-id="9db61-683">1</span><span class="sxs-lookup"><span data-stu-id="9db61-683">1</span></span>| <span data-ttu-id="9db61-684">2</span><span class="sxs-lookup"><span data-stu-id="9db61-684">2</span></span>| <span data-ttu-id="9db61-685">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-685">4</span></span>| <span data-ttu-id="9db61-686">8</span><span class="sxs-lookup"><span data-stu-id="9db61-686">8</span></span>| <span data-ttu-id="9db61-687">16</span><span class="sxs-lookup"><span data-stu-id="9db61-687">16</span></span>| <span data-ttu-id="9db61-688">32</span><span class="sxs-lookup"><span data-stu-id="9db61-688">32</span></span>| <span data-ttu-id="9db61-689">64</span><span class="sxs-lookup"><span data-stu-id="9db61-689">64</span></span>| <span data-ttu-id="9db61-690">64</span><span class="sxs-lookup"><span data-stu-id="9db61-690">64</span></span>|
| <span data-ttu-id="9db61-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="9db61-691">DW6000</span></span> | <span data-ttu-id="9db61-692">32</span><span class="sxs-lookup"><span data-stu-id="9db61-692">32</span></span>| <span data-ttu-id="9db61-693">240</span><span class="sxs-lookup"><span data-stu-id="9db61-693">240</span></span>| <span data-ttu-id="9db61-694">1</span><span class="sxs-lookup"><span data-stu-id="9db61-694">1</span></span>| <span data-ttu-id="9db61-695">2</span><span class="sxs-lookup"><span data-stu-id="9db61-695">2</span></span>| <span data-ttu-id="9db61-696">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-696">4</span></span>| <span data-ttu-id="9db61-697">8</span><span class="sxs-lookup"><span data-stu-id="9db61-697">8</span></span>| <span data-ttu-id="9db61-698">16</span><span class="sxs-lookup"><span data-stu-id="9db61-698">16</span></span>| <span data-ttu-id="9db61-699">32</span><span class="sxs-lookup"><span data-stu-id="9db61-699">32</span></span>| <span data-ttu-id="9db61-700">64</span><span class="sxs-lookup"><span data-stu-id="9db61-700">64</span></span>| <span data-ttu-id="9db61-701">128</span><span class="sxs-lookup"><span data-stu-id="9db61-701">128</span></span>|

<span data-ttu-id="9db61-702">В этих таблицах можно увидеть, что хранилище данных SQL при использовании DW1000 обрабатывает до 32 параллельных запросов и может выделить 40 слотов выдачи.</span><span class="sxs-lookup"><span data-stu-id="9db61-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="9db61-703">Если все пользователи работают с классом smallrc, то будет разрешено выполнять 32 параллельных запроса, так как каждый запрос использует 1 слот выдачи.</span><span class="sxs-lookup"><span data-stu-id="9db61-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="9db61-704">Если всем пользователям DW1000 были запущены в mediumrc, каждый запрос должен размещаться 800 МБ на распространение для выделения общей памяти 47 ГБ каждого запроса и параллелизма бы пользователям ограниченный too5 (40 слоты параллелизма 8 слотов на mediumrc пользователя и).</span><span class="sxs-lookup"><span data-stu-id="9db61-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="9db61-705">Выбор правильного класса ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-705">Selecting proper resource class</span></span>  
<span data-ttu-id="9db61-706">Рекомендуется назначить пользователей toopermanently tooa-класс ресурсов, вместо изменения их классов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="9db61-707">Например таблиц columnstore tooclustered загружает создавать индексы более высокого качества, при выделении памяти.</span><span class="sxs-lookup"><span data-stu-id="9db61-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="9db61-708">tooensure загружает памяти toohigher доступа, создайте пользователя специально для загрузки данных и назначить этого пользователя tooa выше ресурсов класса без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="9db61-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="9db61-709">Существует несколько лучшие методики toofollow здесь.</span><span class="sxs-lookup"><span data-stu-id="9db61-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="9db61-710">Как упоминалось выше, хранилище данных SQL поддерживает два вида типов классов ресурсов: классы статических ресурсов и классы динамических ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="9db61-711">Рекомендации по загрузкам</span><span class="sxs-lookup"><span data-stu-id="9db61-711">Loading best practices</span></span>
1.  <span data-ttu-id="9db61-712">Если ожиданиям hello загрузок с помощью обычных объем данных, класс статический ресурс является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="9db61-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="9db61-713">Позже при масштабировании tooget дополнительные вычислительные возможности, хранилище данных hello, смогут toorun несколько параллельных запрашивает out-of--box, как пользователь нагрузки hello не больше памяти.</span><span class="sxs-lookup"><span data-stu-id="9db61-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="9db61-714">Если полная загружает ожиданиям hello в некоторых случаях, класс динамический ресурс является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="9db61-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="9db61-715">Позже, при вертикальном масштабировании tooget большей вычислительной мощности, hello нагрузки пользователь получит несколько памяти out-of--box, таким образом позволяя tooperform нагрузки hello быстрее.</span><span class="sxs-lookup"><span data-stu-id="9db61-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="9db61-716">Hello загружает tooprocess объем памяти, необходимый эффективно зависит от природы hello загрузить таблицу hello и hello объем обработки данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="9db61-717">Для экземпляра загрузка данных в таблицы CCI требуются некоторые rowgroups CCI toolet памяти достичь оптимальность.</span><span class="sxs-lookup"><span data-stu-id="9db61-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="9db61-718">Дополнительные сведения см. в разделе индексы Columnstore hello - руководство загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="9db61-719">Как правило, мы рекомендуем toouse менее 200 МБ памяти для загрузки.</span><span class="sxs-lookup"><span data-stu-id="9db61-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="9db61-720">Рекомендации по выполнению запросов</span><span class="sxs-lookup"><span data-stu-id="9db61-720">Querying best practices</span></span>
<span data-ttu-id="9db61-721">Запросы имеют различные требования в зависимости от их сложности.</span><span class="sxs-lookup"><span data-stu-id="9db61-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="9db61-722">Увеличить объем памяти для запроса или увеличение параллелизма hello являются оба tooaugment допустимые способы общую пропускную способность, в зависимости от потребностей hello запроса.</span><span class="sxs-lookup"><span data-stu-id="9db61-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="9db61-723">Если hello ожидания обычных, сложные запросы (например, toogenerate ежедневно и еженедельно отчеты) и не обязательно tootake преимуществами параллелизма, класс динамический ресурс является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="9db61-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="9db61-724">Если системе hello tooprocess дополнительные данные, масштабирование hello хранилище данных таким образом автоматически предоставят дополнительные памяти toohello пользователь, выполняющий запрос hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="9db61-725">Если hello ожиданиям, переменной или diurnal паралеллизма (для экземпляра Если hello базы данных запрашивается через веб-интерфейса широко доступны), класс статический ресурс является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="9db61-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="9db61-726">Позже, при масштабировании хранилища toodata hello пользователя, связанного с классом hello статический ресурс будет автоматически быть может toorun несколько параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="9db61-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="9db61-727">Выбор правильного память, в зависимости от необходимости hello запроса не так просто, как он зависит от многих факторов, таких как hello объем данных, запрошенных, hello характер hello схем таблиц и различных соединения, выбора и предикаты группы.</span><span class="sxs-lookup"><span data-stu-id="9db61-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="9db61-728">С точки зрения Общие, выделить больше памяти, позволит toocomplete запросов быстрее, но уменьшится hello общую параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="9db61-729">Если низкий уровень параллелизма не является проблемой, чрезмерное выделение памяти не нанесет вреда.</span><span class="sxs-lookup"><span data-stu-id="9db61-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="9db61-730">может потребоваться toofine настройки пропускной способности при различных конфигурациях ресурсов классов.</span><span class="sxs-lookup"><span data-stu-id="9db61-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="9db61-731">Можно использовать следующие hello хранимой процедуры toofigure out grant параллелизма и памяти на каждый класс ресурсов на заданной цели уровня Обслуживания и hello ближайший наиболее ресурсов класс для операций служб с интенсивными вычислениями CCI памяти для несекционированной таблицы CCI на класс данного ресурса:</span><span class="sxs-lookup"><span data-stu-id="9db61-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="9db61-732">Описание:</span><span class="sxs-lookup"><span data-stu-id="9db61-732">Description:</span></span>  
<span data-ttu-id="9db61-733">Вот hello цель этой хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="9db61-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="9db61-734">toohelp закончится пользователя grant параллелизма и памяти на каждый класс ресурсов на заданной цели.</span><span class="sxs-lookup"><span data-stu-id="9db61-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="9db61-735">Пользователь должен tooprovide значение NULL для схемы и tablename для этого, как показано в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="9db61-736">пользователь toohelp понять, hello ближайший наиболее класс ресурсов для hello памяти intensed CCI операций (нагрузки Копировать таблиц перестроения индекса, т. д.) не секционированной таблицы CCI на класс данного ресурса.</span><span class="sxs-lookup"><span data-stu-id="9db61-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="9db61-737">Hello хранимой процедуры используется toofind схемы таблицы out grant hello требуемый объем памяти для этого.</span><span class="sxs-lookup"><span data-stu-id="9db61-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="9db61-738">Зависимости и ограничения</span><span class="sxs-lookup"><span data-stu-id="9db61-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="9db61-739">Данная хранимая процедура не спроектированных toocalculate требования к памяти для таблицы секционированы cci.</span><span class="sxs-lookup"><span data-stu-id="9db61-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="9db61-740">Данная хранимая процедура не принимает требования к памяти в учетную запись для hello части SELECT CTAS/INSERT-Выбор и предполагает, что он toobe простой запрос SELECT.</span><span class="sxs-lookup"><span data-stu-id="9db61-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="9db61-741">Данная хранимая процедура использует временную таблицу, чтобы это можно было использовать в сеансе hello которой был создан этот хранимая процедура.</span><span class="sxs-lookup"><span data-stu-id="9db61-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="9db61-742">Данная хранимая процедура зависит от текущего предложения hello (например, конфигурации оборудования, DMS конфигурации) и при изменении любого из, затем данная хранимая процедура не будет работать правильно.</span><span class="sxs-lookup"><span data-stu-id="9db61-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="9db61-743">Данная хранимая процедура зависит от существующего предлагаемого ограничения параллелизма, и если он изменится, то данная хранимая процедура будет работать неправильно.</span><span class="sxs-lookup"><span data-stu-id="9db61-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="9db61-744">Данная хранимая процедура зависит от существующих предложений класса ресурсов, и если они изменится, то данная хранимая процедура будет работать неправильно.</span><span class="sxs-lookup"><span data-stu-id="9db61-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="9db61-745">Если вы не получаете выходные данные после выполнения хранимой процедуры с предоставленными параметрами, тогда возможны два варианта.</span><span class="sxs-lookup"><span data-stu-id="9db61-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="9db61-746">1. Один из параметров хранилища данных содержит недопустимое значение SLO.</span><span class="sxs-lookup"><span data-stu-id="9db61-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="9db61-747">2. Отсутствует соответствующий класс ресурсов для операции CCI, если было указано имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="9db61-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="9db61-748">Например в DW100, наибольший предоставления памяти составляет 400 МБ и если таблица имеет схему широкий достаточно toocross hello требование 400 МБ.</span><span class="sxs-lookup"><span data-stu-id="9db61-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="9db61-749">Пример использования</span><span class="sxs-lookup"><span data-stu-id="9db61-749">Usage example:</span></span>
<span data-ttu-id="9db61-750">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="9db61-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="9db61-751">@DWU:Укажите параметр NULL tooextract hello текущей DWU из hello базе данных Хранилища данных или укажите любой поддерживаемый DWU в форме «DW100» hello</span><span class="sxs-lookup"><span data-stu-id="9db61-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="9db61-752">@SCHEMA_NAME:Введите имя схемы таблицы hello</span><span class="sxs-lookup"><span data-stu-id="9db61-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="9db61-753">@TABLE_NAME:Введите имя таблицы, представляющие интерес hello</span><span class="sxs-lookup"><span data-stu-id="9db61-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="9db61-754">Примеры выполнения этой хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="9db61-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="9db61-755">Table1, используемых в hello выше примеры можно рассматривать как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9db61-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="9db61-756">Вот определение hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="9db61-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="9db61-757">Приоритет при выполнении запросов</span><span class="sxs-lookup"><span data-stu-id="9db61-757">Query importance</span></span>
<span data-ttu-id="9db61-758">Классы ресурсов в хранилище данных SQL реализованы с помощью групп рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9db61-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="9db61-759">Существует всего восемь группы рабочей нагрузки, которые управляют поведением hello hello ресурсов классов через hello различных размеров DWU.</span><span class="sxs-lookup"><span data-stu-id="9db61-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="9db61-760">Для любого DWU хранилище данных SQL используется только четыре из восьми групп рабочей нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="9db61-761">Это разумно, так как каждая группа рабочей нагрузки назначен tooone четыре ресурсов классов: smallrc mediumrc, largerc, или xlargerc.</span><span class="sxs-lookup"><span data-stu-id="9db61-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="9db61-762">Hello важность понимания hello группы рабочей нагрузки, что некоторые из этих групп рабочей нагрузки набора toohigher *важность*.</span><span class="sxs-lookup"><span data-stu-id="9db61-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="9db61-763">Значение приоритета используется при планировании распределения ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="9db61-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="9db61-764">Запросы, которым назначен высокий приоритет, получают в три раза больше циклов ЦП, чем запросы со средним приоритетом.</span><span class="sxs-lookup"><span data-stu-id="9db61-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="9db61-765">Поэтому сопоставление слотов выдачи также определяет приоритет ЦП.</span><span class="sxs-lookup"><span data-stu-id="9db61-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="9db61-766">Если для выполнения запроса используется 16 или больше слотов, он помечается как запрос с высоким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="9db61-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="9db61-767">Hello Следующая таблица показывает сопоставления hello важность для каждой группы рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9db61-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="9db61-768">Слоты tooconcurrency сопоставления группы рабочей нагрузки и важности</span><span class="sxs-lookup"><span data-stu-id="9db61-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="9db61-769">Группы рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="9db61-769">Workload groups</span></span> | <span data-ttu-id="9db61-770">Сопоставление слотов выдачи</span><span class="sxs-lookup"><span data-stu-id="9db61-770">Concurrency slot mapping</span></span> | <span data-ttu-id="9db61-771">МБ/распределение</span><span class="sxs-lookup"><span data-stu-id="9db61-771">MB / Distribution</span></span> | <span data-ttu-id="9db61-772">Приоритет</span><span class="sxs-lookup"><span data-stu-id="9db61-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="9db61-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="9db61-773">SloDWGroupC00</span></span> |<span data-ttu-id="9db61-774">1</span><span class="sxs-lookup"><span data-stu-id="9db61-774">1</span></span> |<span data-ttu-id="9db61-775">100</span><span class="sxs-lookup"><span data-stu-id="9db61-775">100</span></span> |<span data-ttu-id="9db61-776">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-776">Medium</span></span> |
| <span data-ttu-id="9db61-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="9db61-777">SloDWGroupC01</span></span> |<span data-ttu-id="9db61-778">2</span><span class="sxs-lookup"><span data-stu-id="9db61-778">2</span></span> |<span data-ttu-id="9db61-779">200</span><span class="sxs-lookup"><span data-stu-id="9db61-779">200</span></span> |<span data-ttu-id="9db61-780">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-780">Medium</span></span> |
| <span data-ttu-id="9db61-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="9db61-781">SloDWGroupC02</span></span> |<span data-ttu-id="9db61-782">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-782">4</span></span> |<span data-ttu-id="9db61-783">400</span><span class="sxs-lookup"><span data-stu-id="9db61-783">400</span></span> |<span data-ttu-id="9db61-784">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-784">Medium</span></span> |
| <span data-ttu-id="9db61-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-785">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-786">8</span><span class="sxs-lookup"><span data-stu-id="9db61-786">8</span></span> |<span data-ttu-id="9db61-787">800</span><span class="sxs-lookup"><span data-stu-id="9db61-787">800</span></span> |<span data-ttu-id="9db61-788">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-788">Medium</span></span> |
| <span data-ttu-id="9db61-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="9db61-789">SloDWGroupC04</span></span> |<span data-ttu-id="9db61-790">16</span><span class="sxs-lookup"><span data-stu-id="9db61-790">16</span></span> |<span data-ttu-id="9db61-791">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-791">1,600</span></span> |<span data-ttu-id="9db61-792">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-792">High</span></span> |
| <span data-ttu-id="9db61-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="9db61-793">SloDWGroupC05</span></span> |<span data-ttu-id="9db61-794">32</span><span class="sxs-lookup"><span data-stu-id="9db61-794">32</span></span> |<span data-ttu-id="9db61-795">3200</span><span class="sxs-lookup"><span data-stu-id="9db61-795">3,200</span></span> |<span data-ttu-id="9db61-796">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-796">High</span></span> |
| <span data-ttu-id="9db61-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="9db61-797">SloDWGroupC06</span></span> |<span data-ttu-id="9db61-798">64</span><span class="sxs-lookup"><span data-stu-id="9db61-798">64</span></span> |<span data-ttu-id="9db61-799">6400</span><span class="sxs-lookup"><span data-stu-id="9db61-799">6,400</span></span> |<span data-ttu-id="9db61-800">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-800">High</span></span> |
| <span data-ttu-id="9db61-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="9db61-801">SloDWGroupC07</span></span> |<span data-ttu-id="9db61-802">128</span><span class="sxs-lookup"><span data-stu-id="9db61-802">128</span></span> |<span data-ttu-id="9db61-803">12 800</span><span class="sxs-lookup"><span data-stu-id="9db61-803">12,800</span></span> |<span data-ttu-id="9db61-804">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-804">High</span></span> |

<span data-ttu-id="9db61-805">Из hello **распределения и потребления слотов параллелизма** диаграммы, можно увидеть, что DW500 используется 1, 4, 8 или 16 параллелизма слотов для smallrc, mediumrc, largerc и xlargerc, соответственно.</span><span class="sxs-lookup"><span data-stu-id="9db61-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="9db61-806">Эти значения можно искать в hello предшествующий важность hello toofind диаграммы для каждого класса ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="9db61-807">Сопоставление DW500 tooimportance классы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="9db61-808">Класс ресурсов</span><span class="sxs-lookup"><span data-stu-id="9db61-808">Resource class</span></span> | <span data-ttu-id="9db61-809">Группа рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="9db61-809">Workload group</span></span> | <span data-ttu-id="9db61-810">Число используемых слотов выдачи</span><span class="sxs-lookup"><span data-stu-id="9db61-810">Concurrency slots used</span></span> | <span data-ttu-id="9db61-811">МБ/распределение</span><span class="sxs-lookup"><span data-stu-id="9db61-811">MB / Distribution</span></span> | <span data-ttu-id="9db61-812">приоритет</span><span class="sxs-lookup"><span data-stu-id="9db61-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="9db61-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="9db61-813">smallrc</span></span> |<span data-ttu-id="9db61-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="9db61-814">SloDWGroupC00</span></span> |<span data-ttu-id="9db61-815">1</span><span class="sxs-lookup"><span data-stu-id="9db61-815">1</span></span> |<span data-ttu-id="9db61-816">100</span><span class="sxs-lookup"><span data-stu-id="9db61-816">100</span></span> |<span data-ttu-id="9db61-817">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-817">Medium</span></span> |
| <span data-ttu-id="9db61-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="9db61-818">mediumrc</span></span> |<span data-ttu-id="9db61-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="9db61-819">SloDWGroupC02</span></span> |<span data-ttu-id="9db61-820">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-820">4</span></span> |<span data-ttu-id="9db61-821">400</span><span class="sxs-lookup"><span data-stu-id="9db61-821">400</span></span> |<span data-ttu-id="9db61-822">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-822">Medium</span></span> |
| <span data-ttu-id="9db61-823">largerc</span><span class="sxs-lookup"><span data-stu-id="9db61-823">largerc</span></span> |<span data-ttu-id="9db61-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-824">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-825">8</span><span class="sxs-lookup"><span data-stu-id="9db61-825">8</span></span> |<span data-ttu-id="9db61-826">800</span><span class="sxs-lookup"><span data-stu-id="9db61-826">800</span></span> |<span data-ttu-id="9db61-827">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-827">Medium</span></span> |
| <span data-ttu-id="9db61-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="9db61-828">xlargerc</span></span> |<span data-ttu-id="9db61-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="9db61-829">SloDWGroupC04</span></span> |<span data-ttu-id="9db61-830">16</span><span class="sxs-lookup"><span data-stu-id="9db61-830">16</span></span> |<span data-ttu-id="9db61-831">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-831">1,600</span></span> |<span data-ttu-id="9db61-832">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-832">High</span></span> |
| <span data-ttu-id="9db61-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="9db61-833">staticrc10</span></span> |<span data-ttu-id="9db61-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="9db61-834">SloDWGroupC00</span></span> |<span data-ttu-id="9db61-835">1</span><span class="sxs-lookup"><span data-stu-id="9db61-835">1</span></span> |<span data-ttu-id="9db61-836">100</span><span class="sxs-lookup"><span data-stu-id="9db61-836">100</span></span> |<span data-ttu-id="9db61-837">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-837">Medium</span></span> |
| <span data-ttu-id="9db61-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="9db61-838">staticrc20</span></span> |<span data-ttu-id="9db61-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="9db61-839">SloDWGroupC01</span></span> |<span data-ttu-id="9db61-840">2</span><span class="sxs-lookup"><span data-stu-id="9db61-840">2</span></span> |<span data-ttu-id="9db61-841">200</span><span class="sxs-lookup"><span data-stu-id="9db61-841">200</span></span> |<span data-ttu-id="9db61-842">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-842">Medium</span></span> |
| <span data-ttu-id="9db61-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="9db61-843">staticrc30</span></span> |<span data-ttu-id="9db61-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="9db61-844">SloDWGroupC02</span></span> |<span data-ttu-id="9db61-845">4.</span><span class="sxs-lookup"><span data-stu-id="9db61-845">4</span></span> |<span data-ttu-id="9db61-846">400</span><span class="sxs-lookup"><span data-stu-id="9db61-846">400</span></span> |<span data-ttu-id="9db61-847">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-847">Medium</span></span> |
| <span data-ttu-id="9db61-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="9db61-848">staticrc40</span></span> |<span data-ttu-id="9db61-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-849">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-850">8</span><span class="sxs-lookup"><span data-stu-id="9db61-850">8</span></span> |<span data-ttu-id="9db61-851">800</span><span class="sxs-lookup"><span data-stu-id="9db61-851">800</span></span> |<span data-ttu-id="9db61-852">Средний</span><span class="sxs-lookup"><span data-stu-id="9db61-852">Medium</span></span> |
| <span data-ttu-id="9db61-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="9db61-853">staticrc50</span></span> |<span data-ttu-id="9db61-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-854">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-855">16</span><span class="sxs-lookup"><span data-stu-id="9db61-855">16</span></span> |<span data-ttu-id="9db61-856">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-856">1,600</span></span> |<span data-ttu-id="9db61-857">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-857">High</span></span> |
| <span data-ttu-id="9db61-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="9db61-858">staticrc60</span></span> |<span data-ttu-id="9db61-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-859">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-860">16</span><span class="sxs-lookup"><span data-stu-id="9db61-860">16</span></span> |<span data-ttu-id="9db61-861">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-861">1,600</span></span> |<span data-ttu-id="9db61-862">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-862">High</span></span> |
| <span data-ttu-id="9db61-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="9db61-863">staticrc70</span></span> |<span data-ttu-id="9db61-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-864">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-865">16</span><span class="sxs-lookup"><span data-stu-id="9db61-865">16</span></span> |<span data-ttu-id="9db61-866">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-866">1,600</span></span> |<span data-ttu-id="9db61-867">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-867">High</span></span> |
| <span data-ttu-id="9db61-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="9db61-868">staticrc80</span></span> |<span data-ttu-id="9db61-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="9db61-869">SloDWGroupC03</span></span> |<span data-ttu-id="9db61-870">16</span><span class="sxs-lookup"><span data-stu-id="9db61-870">16</span></span> |<span data-ttu-id="9db61-871">1 600</span><span class="sxs-lookup"><span data-stu-id="9db61-871">1,600</span></span> |<span data-ttu-id="9db61-872">Высокий</span><span class="sxs-lookup"><span data-stu-id="9db61-872">High</span></span> |

<span data-ttu-id="9db61-873">Можно использовать при устранении неполадок следующие toolook запрос динамического административного Представления в hello различия в выделении ресурсов памяти подробно с точки зрения hello hello регулятора ресурсов или tooanalyze active и за прошедший период использования групп рабочей нагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="9db61-874">Запросы, учитывающие пределы параллелизма</span><span class="sxs-lookup"><span data-stu-id="9db61-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="9db61-875">Большинство запросов управляются классами ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="9db61-876">Эти запросы должен лежать в пределах параллельных запросов hello и пороговые значения слота параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="9db61-877">Пользователь нельзя выбрать tooexclude запроса из модели слот hello параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="9db61-878">tooreiterate, hello следующие инструкции выполнять классов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9db61-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="9db61-879">INSERT SELECT</span><span class="sxs-lookup"><span data-stu-id="9db61-879">INSERT-SELECT</span></span>
* <span data-ttu-id="9db61-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="9db61-880">UPDATE</span></span>
* <span data-ttu-id="9db61-881">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="9db61-881">DELETE</span></span>
* <span data-ttu-id="9db61-882">SELECT (при запросе таблиц пользователя)</span><span class="sxs-lookup"><span data-stu-id="9db61-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="9db61-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="9db61-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="9db61-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="9db61-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="9db61-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="9db61-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="9db61-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="9db61-886">CREATE INDEX</span></span>
* <span data-ttu-id="9db61-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="9db61-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="9db61-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="9db61-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="9db61-889">Загрузка данных</span><span class="sxs-lookup"><span data-stu-id="9db61-889">Data loading</span></span>
* <span data-ttu-id="9db61-890">Операции перемещения данных, осуществляемые hello службы перемещения данных (DMS)</span><span class="sxs-lookup"><span data-stu-id="9db61-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="9db61-891">Запрос исключений tooconcurrency ограничения</span><span class="sxs-lookup"><span data-stu-id="9db61-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="9db61-892">Некоторые запросы не учитывают hello ресурсов класса toowhich hello пользователю назначается.</span><span class="sxs-lookup"><span data-stu-id="9db61-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="9db61-893">Ограничения параллелизма toohello эти исключения при внесении hello ресурсов памяти, необходимый для определенной команды низкое значение, часто из-за hello команда — это операция метаданных.</span><span class="sxs-lookup"><span data-stu-id="9db61-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="9db61-894">Цель Hello эти исключения — tooavoid больше операций выделения памяти для запросов, которые никогда не должны их.</span><span class="sxs-lookup"><span data-stu-id="9db61-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="9db61-895">В таких случаях по умолчанию hello мало ресурсов класса (smallrc) всегда используется независимо от того, класс фактический ресурс hello назначенный пользователь toohello.</span><span class="sxs-lookup"><span data-stu-id="9db61-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="9db61-896">Например, `CREATE LOGIN` всегда будет работать с классом smallrc.</span><span class="sxs-lookup"><span data-stu-id="9db61-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="9db61-897">Hello toofulfill ресурсы, необходимые этой операции являются очень мало, поэтому не вносит в него смысле tooinclude hello запроса в модели слот параллелизма hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="9db61-898">Эти запросы также не ограничивается предел параллелизма пользователя hello 32, неограниченное число таких запросов можно запустить копирование ограничение сеансов toohello 1 024 сеансов.</span><span class="sxs-lookup"><span data-stu-id="9db61-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="9db61-899">Привет, следующие инструкции, не учитывают классов ресурсов:</span><span class="sxs-lookup"><span data-stu-id="9db61-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="9db61-900">CREATE или DROP TABLE;</span><span class="sxs-lookup"><span data-stu-id="9db61-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="9db61-901">ALTER TABLE ... SWITCH, SPLIT или MERGE PARTITION;</span><span class="sxs-lookup"><span data-stu-id="9db61-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="9db61-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="9db61-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="9db61-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="9db61-903">DROP INDEX</span></span>
* <span data-ttu-id="9db61-904">CREATE, UPDATE или DROP STATISTICS;</span><span class="sxs-lookup"><span data-stu-id="9db61-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="9db61-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="9db61-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="9db61-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="9db61-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="9db61-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="9db61-907">CREATE LOGIN</span></span>
* <span data-ttu-id="9db61-908">CREATE, ALTER или DROP USER;</span><span class="sxs-lookup"><span data-stu-id="9db61-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="9db61-909">CREATE, ALTER или DROP PROCEDURE;</span><span class="sxs-lookup"><span data-stu-id="9db61-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="9db61-910">CREATE или DROP VIEW;</span><span class="sxs-lookup"><span data-stu-id="9db61-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="9db61-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="9db61-911">INSERT VALUES</span></span>
* <span data-ttu-id="9db61-912">SELECT (из системных представлений и динамических административных представлений);</span><span class="sxs-lookup"><span data-stu-id="9db61-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="9db61-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="9db61-913">EXPLAIN</span></span>
* <span data-ttu-id="9db61-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="9db61-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="9db61-915"><a name="changing-user-resource-class-example"></a> Пример изменения класса ресурсов пользователя</span><span class="sxs-lookup"><span data-stu-id="9db61-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="9db61-916">**Создайте имя входа:** откройте tooyour подключения **master** базы данных на hello SQL server для размещения базы данных хранилища данных SQL и выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9db61-917">Это разумно toocreate пользователя в базе данных master hello для пользователей в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9db61-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="9db61-918">Создание пользователя в базе данных master позволяет toologin пользователя, с помощью таких средств, как среда SSMS без указания имени базы данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="9db61-919">Он также позволяет им toouse hello объекта обозревателя tooview все базы данных на SQL server.</span><span class="sxs-lookup"><span data-stu-id="9db61-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="9db61-920">Дополнительные сведения о создании пользователей и управлении ими см. в статье [Защита базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9db61-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="9db61-921">**Создание пользователя в хранилище данных SQL:** откройте toohello подключения **хранилище данных SQL** базы данных и выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="9db61-922">**Предоставление разрешений:** hello следующий пример предоставляет `CONTROL` на hello **хранилище данных SQL** базы данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="9db61-923">`CONTROL`в hello уровень базы данных является Здравствуйте, эквивалентные роли db_owner в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9db61-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="9db61-924">**Увеличить класс ресурсов:** используйте hello следующий запрос tooadd tooa выше рабочей нагрузки управления роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="9db61-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="9db61-925">**Уменьшить класс ресурсов:** используйте hello следующий запрос tooremove пользователя из роли управления рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9db61-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9db61-926">Это не возможные tooremove пользователь из smallrc.</span><span class="sxs-lookup"><span data-stu-id="9db61-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="9db61-927">Представление, используемое для определения запросов, поставленных в очередь, и другие динамические административные представления</span><span class="sxs-lookup"><span data-stu-id="9db61-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="9db61-928">Можно использовать hello `sys.dm_pdw_exec_requests` запросы динамического административного Представления tooidentify, ожидающих в очереди с параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="9db61-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="9db61-929">Запросы, ожидающие выделения слота выдачи, будет находиться в **приостановленном**состоянии.</span><span class="sxs-lookup"><span data-stu-id="9db61-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="9db61-930">Чтобы просмотреть роли управления рабочей нагрузкой, можно использовать представление `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="9db61-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="9db61-931">приветствия при следующем запросе показано, какие роли назначается каждому пользователю.</span><span class="sxs-lookup"><span data-stu-id="9db61-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="9db61-932">Хранилище данных SQL имеет следующие hello типах ожидания.</span><span class="sxs-lookup"><span data-stu-id="9db61-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="9db61-933">**LocalQueriesConcurrencyResourceType**: запросы, которые находятся за пределами framework слот hello параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="9db61-934">В качестве примеров таких запросов можно привести запросы и системные функции динамических административных представлений, такие как `SELECT @@VERSION` .</span><span class="sxs-lookup"><span data-stu-id="9db61-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="9db61-935">**UserConcurrencyResourceType**: запросы, которые находятся внутри framework слот hello параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9db61-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="9db61-936">В качестве примеров использования этого типа ресурсов можно привести запросы к таблицам пользователя.</span><span class="sxs-lookup"><span data-stu-id="9db61-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="9db61-937">**DmsConcurrencyResourceType**относится к ожиданиям, связанным с операциями перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="9db61-938">**BackupConcurrencyResourceType**может использоваться при создании резервной копии базы данных.</span><span class="sxs-lookup"><span data-stu-id="9db61-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="9db61-939">Hello максимальное значение для этого типа ресурса равно 1.</span><span class="sxs-lookup"><span data-stu-id="9db61-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="9db61-940">Если несколько операций резервного копирования были запрошены на hello то же время, другим пользователям в очередь hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="9db61-941">Hello `sys.dm_pdw_waits` динамического административного Представления можно использовать toosee, какие ресурсы запрос ожидает.</span><span class="sxs-lookup"><span data-stu-id="9db61-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="9db61-942">Hello `sys.dm_pdw_resource_waits` динамическое административное Представление показывает только ожидания hello ресурсов, потребляемых данного запроса.</span><span class="sxs-lookup"><span data-stu-id="9db61-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="9db61-943">Время ожидания ресурса только измеряет hello времени ожидания ресурсов toobe указано, как противоположность toosignal ожидания времени, которое hello время, необходимое для hello базовый запрос hello tooschedule серверы SQL на ЦП hello.</span><span class="sxs-lookup"><span data-stu-id="9db61-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="9db61-944">Hello `sys.dm_pdw_wait_stats` динамического административного Представления можно использовать для анализа исторических тенденций ожиданий.</span><span class="sxs-lookup"><span data-stu-id="9db61-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="9db61-945">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9db61-945">Next steps</span></span>
<span data-ttu-id="9db61-946">Дополнительные сведения об управлении пользователями и безопасностью базы данных см. в статье [Защита базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9db61-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="9db61-947">Дополнительные сведения о классах большие ресурсов может повысить качество кластеризованный индекс, см. в разделе [перестроение индексов tooimprove сегмент качество].</span><span class="sxs-lookup"><span data-stu-id="9db61-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[перестроение индексов tooimprove сегмент качество]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
