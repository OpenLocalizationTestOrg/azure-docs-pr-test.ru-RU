---
title: "Управление вычислительными ресурсами в хранилище данных SQL Azure (общие сведения) | Документация Майкрософт"
description: "Возможности масштабирования производительности в хранилище данных SQL Azure. Вы можете увеличивать масштаб, изменяя объем DWU, а также приостанавливать и возобновлять работу вычислительных ресурсов для сокращения затрат."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="80d04-104">Управление вычислительными ресурсами в хранилище данных SQL Azure (обзор)</span><span class="sxs-lookup"><span data-stu-id="80d04-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80d04-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="80d04-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="80d04-106">Портал</span><span class="sxs-lookup"><span data-stu-id="80d04-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="80d04-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80d04-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="80d04-108">REST</span><span class="sxs-lookup"><span data-stu-id="80d04-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="80d04-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="80d04-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="80d04-110">Архитектура хранилища данных SQL разделяет хранилище и вычислительные ресурсы, что позволяет масштабировать их независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="80d04-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="80d04-111">В результате можно масштабировать вычислительные ресурсы в соответствии с требованиями к производительности независимо от объема данных.</span><span class="sxs-lookup"><span data-stu-id="80d04-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="80d04-112">При такой архитектуре [выставление счетов][billed] за ресурсы вычисления и хранения осуществляется отдельно.</span><span class="sxs-lookup"><span data-stu-id="80d04-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="80d04-113">В этом обзоре рассматриваются возможности масштабирования для хранилища данных SQL и сведения о том, как использовать возможности приостановления, возобновления и масштабирования хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="80d04-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="80d04-114">Сведения о том, как связаны единицы DWU и производительность, см. в разделе [Прогнозируемая и масштабируемая производительность и единицы использования хранилища данных][data warehouse units (DWUs)].</span><span class="sxs-lookup"><span data-stu-id="80d04-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="80d04-115">Как работают операции управления вычислениями в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="80d04-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="80d04-116">Архитектура хранилища данных SQL состоит из управляющего узла, вычислительных узлов и уровня хранилища, разделенного между 60 распределениями.</span><span class="sxs-lookup"><span data-stu-id="80d04-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="80d04-117">Во время обычного активного сеанса в хранилище данных SQL головной узел системы управляет метаданными и содержит оптимизатор распределенных запросов.</span><span class="sxs-lookup"><span data-stu-id="80d04-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="80d04-118">Вычислительные узлы и уровень хранилища размещены под головным узлом.</span><span class="sxs-lookup"><span data-stu-id="80d04-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="80d04-119">При 400 DWU система включает в себя один головной узел, четыре вычислительных узла и уровень хранилища, состоящий из 60 распределений.</span><span class="sxs-lookup"><span data-stu-id="80d04-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="80d04-120">Если выполняется операция масштабирования или приостановки, система сначала уничтожает все входящие запросы, а затем выполняет откат транзакций, чтобы обеспечить стабильное состояние.</span><span class="sxs-lookup"><span data-stu-id="80d04-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="80d04-121">Операции масштабирования можно выполнить только после завершения отката транзакций.</span><span class="sxs-lookup"><span data-stu-id="80d04-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="80d04-122">При операции увеличения масштаба система подготавливает нужное количество вычислительных узлов, после чего присоединяет их к уровню хранилища.</span><span class="sxs-lookup"><span data-stu-id="80d04-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="80d04-123">При операции уменьшения масштаба ненужные узлы освобождаются, а оставшиеся вычислительные узлы заново присоединяются к нужному количеству распределений.</span><span class="sxs-lookup"><span data-stu-id="80d04-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="80d04-124">При операции приостановки все вычислительные узлы освобождаются, а система выполняет различные операции метаданных, чтобы итоговая система находилась в стабильном состоянии.</span><span class="sxs-lookup"><span data-stu-id="80d04-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="80d04-125">DWU</span><span class="sxs-lookup"><span data-stu-id="80d04-125">DWU</span></span>  | <span data-ttu-id="80d04-126">\# вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="80d04-126">\#of compute nodes</span></span> | <span data-ttu-id="80d04-127">\# распределений на узел</span><span class="sxs-lookup"><span data-stu-id="80d04-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="80d04-128">100</span><span class="sxs-lookup"><span data-stu-id="80d04-128">100</span></span>  | <span data-ttu-id="80d04-129">1</span><span class="sxs-lookup"><span data-stu-id="80d04-129">1</span></span>                  | <span data-ttu-id="80d04-130">60</span><span class="sxs-lookup"><span data-stu-id="80d04-130">60</span></span>                           |
| <span data-ttu-id="80d04-131">200</span><span class="sxs-lookup"><span data-stu-id="80d04-131">200</span></span>  | <span data-ttu-id="80d04-132">2</span><span class="sxs-lookup"><span data-stu-id="80d04-132">2</span></span>                  | <span data-ttu-id="80d04-133">30</span><span class="sxs-lookup"><span data-stu-id="80d04-133">30</span></span>                           |
| <span data-ttu-id="80d04-134">300</span><span class="sxs-lookup"><span data-stu-id="80d04-134">300</span></span>  | <span data-ttu-id="80d04-135">3</span><span class="sxs-lookup"><span data-stu-id="80d04-135">3</span></span>                  | <span data-ttu-id="80d04-136">20</span><span class="sxs-lookup"><span data-stu-id="80d04-136">20</span></span>                           |
| <span data-ttu-id="80d04-137">400</span><span class="sxs-lookup"><span data-stu-id="80d04-137">400</span></span>  | <span data-ttu-id="80d04-138">4.</span><span class="sxs-lookup"><span data-stu-id="80d04-138">4</span></span>                  | <span data-ttu-id="80d04-139">15</span><span class="sxs-lookup"><span data-stu-id="80d04-139">15</span></span>                           |
| <span data-ttu-id="80d04-140">500</span><span class="sxs-lookup"><span data-stu-id="80d04-140">500</span></span>  | <span data-ttu-id="80d04-141">5</span><span class="sxs-lookup"><span data-stu-id="80d04-141">5</span></span>                  | <span data-ttu-id="80d04-142">12</span><span class="sxs-lookup"><span data-stu-id="80d04-142">12</span></span>                           |
| <span data-ttu-id="80d04-143">600</span><span class="sxs-lookup"><span data-stu-id="80d04-143">600</span></span>  | <span data-ttu-id="80d04-144">6</span><span class="sxs-lookup"><span data-stu-id="80d04-144">6</span></span>                  | <span data-ttu-id="80d04-145">10</span><span class="sxs-lookup"><span data-stu-id="80d04-145">10</span></span>                           |
| <span data-ttu-id="80d04-146">1000</span><span class="sxs-lookup"><span data-stu-id="80d04-146">1000</span></span> | <span data-ttu-id="80d04-147">10</span><span class="sxs-lookup"><span data-stu-id="80d04-147">10</span></span>                 | <span data-ttu-id="80d04-148">6</span><span class="sxs-lookup"><span data-stu-id="80d04-148">6</span></span>                            |
| <span data-ttu-id="80d04-149">1200</span><span class="sxs-lookup"><span data-stu-id="80d04-149">1200</span></span> | <span data-ttu-id="80d04-150">12</span><span class="sxs-lookup"><span data-stu-id="80d04-150">12</span></span>                 | <span data-ttu-id="80d04-151">5</span><span class="sxs-lookup"><span data-stu-id="80d04-151">5</span></span>                            |
| <span data-ttu-id="80d04-152">1500</span><span class="sxs-lookup"><span data-stu-id="80d04-152">1500</span></span> | <span data-ttu-id="80d04-153">15</span><span class="sxs-lookup"><span data-stu-id="80d04-153">15</span></span>                 | <span data-ttu-id="80d04-154">4</span><span class="sxs-lookup"><span data-stu-id="80d04-154">4</span></span>                            |
| <span data-ttu-id="80d04-155">2000</span><span class="sxs-lookup"><span data-stu-id="80d04-155">2000</span></span> | <span data-ttu-id="80d04-156">20</span><span class="sxs-lookup"><span data-stu-id="80d04-156">20</span></span>                 | <span data-ttu-id="80d04-157">3</span><span class="sxs-lookup"><span data-stu-id="80d04-157">3</span></span>                            |
| <span data-ttu-id="80d04-158">3000</span><span class="sxs-lookup"><span data-stu-id="80d04-158">3000</span></span> | <span data-ttu-id="80d04-159">30</span><span class="sxs-lookup"><span data-stu-id="80d04-159">30</span></span>                 | <span data-ttu-id="80d04-160">2</span><span class="sxs-lookup"><span data-stu-id="80d04-160">2</span></span>                            |
| <span data-ttu-id="80d04-161">6000</span><span class="sxs-lookup"><span data-stu-id="80d04-161">6000</span></span> | <span data-ttu-id="80d04-162">60</span><span class="sxs-lookup"><span data-stu-id="80d04-162">60</span></span>                 | <span data-ttu-id="80d04-163">1</span><span class="sxs-lookup"><span data-stu-id="80d04-163">1</span></span>                            |

<span data-ttu-id="80d04-164">Ниже перечислены три основные функции управления вычислениями.</span><span class="sxs-lookup"><span data-stu-id="80d04-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="80d04-165">Приостановить</span><span class="sxs-lookup"><span data-stu-id="80d04-165">Pause</span></span>
2. <span data-ttu-id="80d04-166">Продолжить</span><span class="sxs-lookup"><span data-stu-id="80d04-166">Resume</span></span>
3. <span data-ttu-id="80d04-167">Масштаб</span><span class="sxs-lookup"><span data-stu-id="80d04-167">Scale</span></span>

<span data-ttu-id="80d04-168">Выполнение каждой из этих операций может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="80d04-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="80d04-169">Если операции масштабирования, приостановки и возобновления выполняются автоматически, можно реализовать логику, позволяющую приступать к выполнению другого действия только после завершения определенных операций.</span><span class="sxs-lookup"><span data-stu-id="80d04-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="80d04-170">Проверка состояния базы данных с использованием различных конечных точек позволяет правильно реализовать автоматизацию этих операций.</span><span class="sxs-lookup"><span data-stu-id="80d04-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="80d04-171">На портале отображается уведомление о завершении операции и текущее состояние баз данных, однако здесь нельзя проверять состояние программным способом.</span><span class="sxs-lookup"><span data-stu-id="80d04-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="80d04-172">Функцию управления вычислениями можно выполнять не для всех конечных точек.</span><span class="sxs-lookup"><span data-stu-id="80d04-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="80d04-173">Приостановка и возобновление</span><span class="sxs-lookup"><span data-stu-id="80d04-173">Pause/Resume</span></span> | <span data-ttu-id="80d04-174">Масштаб</span><span class="sxs-lookup"><span data-stu-id="80d04-174">Scale</span></span> | <span data-ttu-id="80d04-175">Проверка состояния базы данных</span><span class="sxs-lookup"><span data-stu-id="80d04-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="80d04-176">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="80d04-176">Azure portal</span></span> | <span data-ttu-id="80d04-177">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-177">Yes</span></span>          | <span data-ttu-id="80d04-178">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-178">Yes</span></span>   | <span data-ttu-id="80d04-179">**Нет**</span><span class="sxs-lookup"><span data-stu-id="80d04-179">**No**</span></span>               |
| <span data-ttu-id="80d04-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80d04-180">PowerShell</span></span>   | <span data-ttu-id="80d04-181">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-181">Yes</span></span>          | <span data-ttu-id="80d04-182">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-182">Yes</span></span>   | <span data-ttu-id="80d04-183">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-183">Yes</span></span>                  |
| <span data-ttu-id="80d04-184">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="80d04-184">REST API</span></span>     | <span data-ttu-id="80d04-185">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-185">Yes</span></span>          | <span data-ttu-id="80d04-186">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-186">Yes</span></span>   | <span data-ttu-id="80d04-187">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-187">Yes</span></span>                  |
| <span data-ttu-id="80d04-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="80d04-188">T-SQL</span></span>        | <span data-ttu-id="80d04-189">**Нет**</span><span class="sxs-lookup"><span data-stu-id="80d04-189">**No**</span></span>       | <span data-ttu-id="80d04-190">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-190">Yes</span></span>   | <span data-ttu-id="80d04-191">Да</span><span class="sxs-lookup"><span data-stu-id="80d04-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="80d04-192">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="80d04-192">Scale compute</span></span>

<span data-ttu-id="80d04-193">Производительность в хранилище данных SQL измеряется в [единицах использования хранилища данных (DWU)][data warehouse units (DWUs)], которые являются абстрактной мерой вычислительных ресурсов, таких как ЦП, память и пропускная способность ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="80d04-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="80d04-194">Вы можете масштабировать производительность системы с помощью различных средств, таких как портал, T-SQL и REST API.</span><span class="sxs-lookup"><span data-stu-id="80d04-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="80d04-195">Как масштабировать вычислительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="80d04-195">How do I scale compute?</span></span>
<span data-ttu-id="80d04-196">Масштабирование вычислительных ресурсов в хранилище данных SQL осуществляется путем изменения параметра DWU.</span><span class="sxs-lookup"><span data-stu-id="80d04-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="80d04-197">При добавлении дополнительных DWU для некоторых операций производительность будет повышаться [линейно][linearly].</span><span class="sxs-lookup"><span data-stu-id="80d04-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="80d04-198">Мы разработали предложения DWU, благодаря которым ваша производительность заметно изменится при уменьшении или увеличении масштаба системы.</span><span class="sxs-lookup"><span data-stu-id="80d04-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="80d04-199">Для настройки DWU можно использовать любые из следующих отдельных методов:</span><span class="sxs-lookup"><span data-stu-id="80d04-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="80d04-200">[Масштабирование вычислительных ресурсов с помощью портала Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="80d04-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="80d04-201">[Масштабирование вычислительных ресурсов с помощью PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="80d04-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="80d04-202">[Масштабирование вычислительных ресурсов с помощью REST API][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="80d04-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="80d04-203">[Масштабирование вычислительных ресурсов с помощью TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="80d04-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="80d04-204">Сколько DWU нужно использовать</span><span class="sxs-lookup"><span data-stu-id="80d04-204">How many DWUs should I use?</span></span>

<span data-ttu-id="80d04-205">Чтобы определить оптимальное значение DWU, попробуйте увеличить и уменьшить масштаб, а также выполнить несколько запросов после загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="80d04-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="80d04-206">Так как масштабирование выполняется достаточно быстро, попробуйте использовать разные уровни производительности не дольше одного часа.</span><span class="sxs-lookup"><span data-stu-id="80d04-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="80d04-207">Хранилище данных SQL предназначено для обработки больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="80d04-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="80d04-208">Чтобы определить реальные возможности масштабирования (для больших значений DWU), вы можете использовать большой набор данных, размер которого достигает или превышает 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="80d04-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="80d04-209">Рекомендации по выборе оптимального объема DWU для рабочей нагрузки:</span><span class="sxs-lookup"><span data-stu-id="80d04-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="80d04-210">Если хранилище данных только создается, начните с небольшого уровня производительности, обеспечиваемого DWU.</span><span class="sxs-lookup"><span data-stu-id="80d04-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="80d04-211">В качестве отправной точки можно использовать DW400 или DW200.</span><span class="sxs-lookup"><span data-stu-id="80d04-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="80d04-212">Отслеживайте производительность приложения, сравнивая ее с количеством выбранных DWU.</span><span class="sxs-lookup"><span data-stu-id="80d04-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="80d04-213">Определите, насколько выше или ниже должна быть производительность, которая оптимально соответствует требуемому вам уровню (учитывайте линейное масштабирование).</span><span class="sxs-lookup"><span data-stu-id="80d04-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="80d04-214">Увеличьте или уменьшите число DWU в соответствии с тем, насколько вы хотите увеличить или уменьшить скорость выполнения вашей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="80d04-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="80d04-215">Вносите изменения, пока не достигнете уровня производительности, который оптимально отвечает вашим бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="80d04-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="80d04-216">Высокий уровень параллелизма только увеличивает производительность обработки запросов, если нагрузку можно разделить между вычислительными узлами.</span><span class="sxs-lookup"><span data-stu-id="80d04-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="80d04-217">Если вы обнаружили, что масштабирование не влияет на производительность, ознакомьтесь со статьями о настройке производительности, чтобы проверить, распределены ли данные неравномерно или не перемещаете ли вы большой объем данных.</span><span class="sxs-lookup"><span data-stu-id="80d04-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="80d04-218">Когда следует масштабировать DWU</span><span class="sxs-lookup"><span data-stu-id="80d04-218">When should I scale DWUs?</span></span>
<span data-ttu-id="80d04-219">Масштабирование единиц DWU изменяет следующие важные сценарии:</span><span class="sxs-lookup"><span data-stu-id="80d04-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="80d04-220">Линейное изменение производительности системы для операций сканирования, агрегирования и инструкций CTAS.</span><span class="sxs-lookup"><span data-stu-id="80d04-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="80d04-221">Увеличение количества модулей чтения и записи при загрузке с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="80d04-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="80d04-222">Максимальное количество параллельных запросов и слотов выдачи.</span><span class="sxs-lookup"><span data-stu-id="80d04-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="80d04-223">Рекомендации по выборе времени для масштабирования DWU</span><span class="sxs-lookup"><span data-stu-id="80d04-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="80d04-224">Прежде чем выполнять ресурсоемкую загрузку данных или их преобразование, увеличьте объем DWU, чтобы быстрее получать доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="80d04-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="80d04-225">Во время рабочих часов наибольшей нагрузки выполните масштабирование, чтобы обработать большое количество одновременных запросов.</span><span class="sxs-lookup"><span data-stu-id="80d04-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="80d04-226">Приостановка работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="80d04-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="80d04-227">Для приостановки базы данных можно использовать любые из следующих отдельных методов:</span><span class="sxs-lookup"><span data-stu-id="80d04-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="80d04-228">[Приостановка работы вычислительных ресурсов с помощью портала Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="80d04-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="80d04-229">[Приостановка работы вычислительных ресурсов с помощью PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="80d04-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="80d04-230">[Приостановка работы вычислительных ресурсов с помощью REST API][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="80d04-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="80d04-231">Возобновление работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="80d04-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="80d04-232">Для возобновления базы данных можно использовать любые из следующих отдельных методов:</span><span class="sxs-lookup"><span data-stu-id="80d04-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="80d04-233">[Возобновление работы вычислительных ресурсов с помощью портала Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="80d04-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="80d04-234">[Возобновление работы вычислительных ресурсов с помощью PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="80d04-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="80d04-235">[Возобновление работы вычислительных ресурсов с помощью REST API][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="80d04-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="80d04-236">Проверка состояния базы данных</span><span class="sxs-lookup"><span data-stu-id="80d04-236">Check database state</span></span> 

<span data-ttu-id="80d04-237">Для возобновления базы данных можно использовать любые из следующих отдельных методов:</span><span class="sxs-lookup"><span data-stu-id="80d04-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="80d04-238">[проверка состояния базы данных с помощью T-SQL;][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="80d04-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="80d04-239">[проверка состояния базы данных с помощью PowerShell;][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="80d04-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="80d04-240">[проверка состояния базы данных с помощью REST API.][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="80d04-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="80d04-241">Разрешения</span><span class="sxs-lookup"><span data-stu-id="80d04-241">Permissions</span></span>

<span data-ttu-id="80d04-242">Для масштабирования базы данных потребуются разрешения, описанные в статье [Изменение базы данных (хранилище данных Azure SQL)][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="80d04-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="80d04-243">Чтобы приостановить и возобновить работу, нужны разрешения [Участник баз данных SQL][SQL DB Contributor], в частности Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="80d04-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="80d04-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80d04-244">Next steps</span></span>
<span data-ttu-id="80d04-245">Приведенные ниже статьи помогут вам разобраться с некоторыми дополнительными ключевыми понятиями, связанными с производительностью:</span><span class="sxs-lookup"><span data-stu-id="80d04-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="80d04-246">[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="80d04-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="80d04-247">[Общие сведения о таблицах в хранилище данных SQL][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="80d04-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="80d04-248">[Распределение таблиц в хранилище данных SQL][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="80d04-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="80d04-249">[Indexing tables in SQL Data Warehouse (Индексирование таблиц в хранилище данных SQL)][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="80d04-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="80d04-250">[Секционирование таблиц в хранилище данных SQL][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="80d04-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="80d04-251">[Управление статистикой таблиц в хранилище данных SQL][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="80d04-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="80d04-252">[Рекомендации по использованию хранилища данных SQL Azure][Best practices]</span><span class="sxs-lookup"><span data-stu-id="80d04-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
