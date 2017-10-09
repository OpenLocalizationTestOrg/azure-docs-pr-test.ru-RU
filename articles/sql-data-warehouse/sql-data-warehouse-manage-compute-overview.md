---
title: "aaaManage вычислительная мощность в хранилище данных SQL Azure (Обзор) | Документы Microsoft"
description: "Возможности масштабирования производительности в хранилище данных SQL Azure. Горизонтальное масштабирование, перемещая Dwu или приостанавливать и возобновлять toosave затраты вычислительных ресурсов."
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
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="f75de-104">Управление вычислительными ресурсами в хранилище данных SQL Azure (обзор)</span><span class="sxs-lookup"><span data-stu-id="f75de-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f75de-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="f75de-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="f75de-106">Портал</span><span class="sxs-lookup"><span data-stu-id="f75de-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="f75de-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f75de-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="f75de-108">REST</span><span class="sxs-lookup"><span data-stu-id="f75de-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="f75de-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="f75de-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="f75de-110">Hello архитектура хранилища данных SQL отделяет хранилища и вычислений, позволяя каждого tooscale независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="f75de-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="f75de-111">В результате вычислений может быть требований к производительности масштабированный toomeet независимо от hello объем данных.</span><span class="sxs-lookup"><span data-stu-id="f75de-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="f75de-112">При такой архитектуре [выставление счетов][billed] за ресурсы вычисления и хранения осуществляется отдельно.</span><span class="sxs-lookup"><span data-stu-id="f75de-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="f75de-113">В этом обзоре описываются как горизонтальное масштабирование работает с хранилищем данных SQL и как tooutilize hello приостановки, возобновления и возможности масштабирования хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="f75de-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="f75de-114">Обратитесь к hello [единицы (Dwu) в хранилище данных] [ data warehouse units (DWUs)] toolearn страницы, как связаны Dwu и производительности.</span><span class="sxs-lookup"><span data-stu-id="f75de-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="f75de-115">Как работают операции управления вычислениями в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="f75de-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="f75de-116">Архитектура Hello для хранилища данных SQL состоит из узла управления, вычислительных узлов и hello распределяться 60 распределения уровня хранилища.</span><span class="sxs-lookup"><span data-stu-id="f75de-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="f75de-117">Во время обычной активного сеанса в хранилище данных SQL головной узел системы управляет метаданными hello и содержит оптимизатор hello распределенных запросов.</span><span class="sxs-lookup"><span data-stu-id="f75de-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="f75de-118">Вычислительные узлы и уровень хранилища размещены под головным узлом.</span><span class="sxs-lookup"><span data-stu-id="f75de-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="f75de-119">400 DWU в системе установлены одного головного узла, четыре вычислительных узлов и уровень хранилища hello, состоящий из 60 распределения.</span><span class="sxs-lookup"><span data-stu-id="f75de-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="f75de-120">Когда быть тщательно проанализирован на шкале или приостанавливать операции, система hello сначала разрывает все входящие запросы и откатывает транзакции tooensure согласованное состояние.</span><span class="sxs-lookup"><span data-stu-id="f75de-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="f75de-121">Операции масштабирования можно выполнить только после завершения отката транзакций.</span><span class="sxs-lookup"><span data-stu-id="f75de-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="f75de-122">Для операции масштабирования Подготовка системы hello hello лишние нужное количество вычислительных узлов и затем начинает повторное присоединение слой hello вычислительных узлов toohello хранилища.</span><span class="sxs-lookup"><span data-stu-id="f75de-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="f75de-123">Для операции уменьшения масштаба hello ненужные узлы освобождаются и hello оставшиеся вычислительные узлы заново присоединить сами toohello соответствующего числа распределений.</span><span class="sxs-lookup"><span data-stu-id="f75de-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="f75de-124">Для операции приостановки все вычислительные узлы выпущены и системы подвергнется разнообразные операции tooleave метаданных окончательного системы в устойчивом состоянии.</span><span class="sxs-lookup"><span data-stu-id="f75de-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="f75de-125">DWU</span><span class="sxs-lookup"><span data-stu-id="f75de-125">DWU</span></span>  | <span data-ttu-id="f75de-126">\# вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="f75de-126">\#of compute nodes</span></span> | <span data-ttu-id="f75de-127">\# распределений на узел</span><span class="sxs-lookup"><span data-stu-id="f75de-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="f75de-128">100</span><span class="sxs-lookup"><span data-stu-id="f75de-128">100</span></span>  | <span data-ttu-id="f75de-129">1</span><span class="sxs-lookup"><span data-stu-id="f75de-129">1</span></span>                  | <span data-ttu-id="f75de-130">60</span><span class="sxs-lookup"><span data-stu-id="f75de-130">60</span></span>                           |
| <span data-ttu-id="f75de-131">200</span><span class="sxs-lookup"><span data-stu-id="f75de-131">200</span></span>  | <span data-ttu-id="f75de-132">2</span><span class="sxs-lookup"><span data-stu-id="f75de-132">2</span></span>                  | <span data-ttu-id="f75de-133">30</span><span class="sxs-lookup"><span data-stu-id="f75de-133">30</span></span>                           |
| <span data-ttu-id="f75de-134">300</span><span class="sxs-lookup"><span data-stu-id="f75de-134">300</span></span>  | <span data-ttu-id="f75de-135">3</span><span class="sxs-lookup"><span data-stu-id="f75de-135">3</span></span>                  | <span data-ttu-id="f75de-136">20</span><span class="sxs-lookup"><span data-stu-id="f75de-136">20</span></span>                           |
| <span data-ttu-id="f75de-137">400</span><span class="sxs-lookup"><span data-stu-id="f75de-137">400</span></span>  | <span data-ttu-id="f75de-138">4.</span><span class="sxs-lookup"><span data-stu-id="f75de-138">4</span></span>                  | <span data-ttu-id="f75de-139">15</span><span class="sxs-lookup"><span data-stu-id="f75de-139">15</span></span>                           |
| <span data-ttu-id="f75de-140">500</span><span class="sxs-lookup"><span data-stu-id="f75de-140">500</span></span>  | <span data-ttu-id="f75de-141">5</span><span class="sxs-lookup"><span data-stu-id="f75de-141">5</span></span>                  | <span data-ttu-id="f75de-142">12</span><span class="sxs-lookup"><span data-stu-id="f75de-142">12</span></span>                           |
| <span data-ttu-id="f75de-143">600</span><span class="sxs-lookup"><span data-stu-id="f75de-143">600</span></span>  | <span data-ttu-id="f75de-144">6</span><span class="sxs-lookup"><span data-stu-id="f75de-144">6</span></span>                  | <span data-ttu-id="f75de-145">10</span><span class="sxs-lookup"><span data-stu-id="f75de-145">10</span></span>                           |
| <span data-ttu-id="f75de-146">1000</span><span class="sxs-lookup"><span data-stu-id="f75de-146">1000</span></span> | <span data-ttu-id="f75de-147">10</span><span class="sxs-lookup"><span data-stu-id="f75de-147">10</span></span>                 | <span data-ttu-id="f75de-148">6</span><span class="sxs-lookup"><span data-stu-id="f75de-148">6</span></span>                            |
| <span data-ttu-id="f75de-149">1200</span><span class="sxs-lookup"><span data-stu-id="f75de-149">1200</span></span> | <span data-ttu-id="f75de-150">12</span><span class="sxs-lookup"><span data-stu-id="f75de-150">12</span></span>                 | <span data-ttu-id="f75de-151">5</span><span class="sxs-lookup"><span data-stu-id="f75de-151">5</span></span>                            |
| <span data-ttu-id="f75de-152">1500</span><span class="sxs-lookup"><span data-stu-id="f75de-152">1500</span></span> | <span data-ttu-id="f75de-153">15</span><span class="sxs-lookup"><span data-stu-id="f75de-153">15</span></span>                 | <span data-ttu-id="f75de-154">4</span><span class="sxs-lookup"><span data-stu-id="f75de-154">4</span></span>                            |
| <span data-ttu-id="f75de-155">2000</span><span class="sxs-lookup"><span data-stu-id="f75de-155">2000</span></span> | <span data-ttu-id="f75de-156">20</span><span class="sxs-lookup"><span data-stu-id="f75de-156">20</span></span>                 | <span data-ttu-id="f75de-157">3</span><span class="sxs-lookup"><span data-stu-id="f75de-157">3</span></span>                            |
| <span data-ttu-id="f75de-158">3000</span><span class="sxs-lookup"><span data-stu-id="f75de-158">3000</span></span> | <span data-ttu-id="f75de-159">30</span><span class="sxs-lookup"><span data-stu-id="f75de-159">30</span></span>                 | <span data-ttu-id="f75de-160">2</span><span class="sxs-lookup"><span data-stu-id="f75de-160">2</span></span>                            |
| <span data-ttu-id="f75de-161">6000</span><span class="sxs-lookup"><span data-stu-id="f75de-161">6000</span></span> | <span data-ttu-id="f75de-162">60</span><span class="sxs-lookup"><span data-stu-id="f75de-162">60</span></span>                 | <span data-ttu-id="f75de-163">1</span><span class="sxs-lookup"><span data-stu-id="f75de-163">1</span></span>                            |

<span data-ttu-id="f75de-164">Hello три основные функции управления вычислений —:</span><span class="sxs-lookup"><span data-stu-id="f75de-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="f75de-165">Приостановить</span><span class="sxs-lookup"><span data-stu-id="f75de-165">Pause</span></span>
2. <span data-ttu-id="f75de-166">Продолжить</span><span class="sxs-lookup"><span data-stu-id="f75de-166">Resume</span></span>
3. <span data-ttu-id="f75de-167">Масштаб</span><span class="sxs-lookup"><span data-stu-id="f75de-167">Scale</span></span>

<span data-ttu-id="f75de-168">Каждый из этих операций может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f75de-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="f75de-169">Если масштабирование или приостановка и возобновление работы автоматически, вы можете tooimplement логику tooensure что некоторые операции были завершены перед выполнением другого действия.</span><span class="sxs-lookup"><span data-stu-id="f75de-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="f75de-170">Проверка состояния базы данных hello через различные конечные точки можно toocorrectly реализация автоматизации таких операций.</span><span class="sxs-lookup"><span data-stu-id="f75de-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="f75de-171">Hello портал предоставляет уведомление о завершении операции и hello базы данных текущее состояние, но не допускает программный о проверке состояния.</span><span class="sxs-lookup"><span data-stu-id="f75de-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="f75de-172">Функцию управления вычислениями можно выполнять не для всех конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f75de-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="f75de-173">Приостановка и возобновление</span><span class="sxs-lookup"><span data-stu-id="f75de-173">Pause/Resume</span></span> | <span data-ttu-id="f75de-174">Масштаб</span><span class="sxs-lookup"><span data-stu-id="f75de-174">Scale</span></span> | <span data-ttu-id="f75de-175">Проверка состояния базы данных</span><span class="sxs-lookup"><span data-stu-id="f75de-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="f75de-176">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f75de-176">Azure portal</span></span> | <span data-ttu-id="f75de-177">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-177">Yes</span></span>          | <span data-ttu-id="f75de-178">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-178">Yes</span></span>   | <span data-ttu-id="f75de-179">**Нет**</span><span class="sxs-lookup"><span data-stu-id="f75de-179">**No**</span></span>               |
| <span data-ttu-id="f75de-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f75de-180">PowerShell</span></span>   | <span data-ttu-id="f75de-181">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-181">Yes</span></span>          | <span data-ttu-id="f75de-182">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-182">Yes</span></span>   | <span data-ttu-id="f75de-183">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-183">Yes</span></span>                  |
| <span data-ttu-id="f75de-184">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="f75de-184">REST API</span></span>     | <span data-ttu-id="f75de-185">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-185">Yes</span></span>          | <span data-ttu-id="f75de-186">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-186">Yes</span></span>   | <span data-ttu-id="f75de-187">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-187">Yes</span></span>                  |
| <span data-ttu-id="f75de-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="f75de-188">T-SQL</span></span>        | <span data-ttu-id="f75de-189">**Нет**</span><span class="sxs-lookup"><span data-stu-id="f75de-189">**No**</span></span>       | <span data-ttu-id="f75de-190">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-190">Yes</span></span>   | <span data-ttu-id="f75de-191">Да</span><span class="sxs-lookup"><span data-stu-id="f75de-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="f75de-192">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="f75de-192">Scale compute</span></span>

<span data-ttu-id="f75de-193">Производительность в хранилище данных SQL измеряется в [единицах использования хранилища данных (DWU)][data warehouse units (DWUs)], которые являются абстрактной мерой вычислительных ресурсов, таких как ЦП, память и пропускная способность ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="f75de-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="f75de-194">Пользователь, который хотел tooscale производительность свои системы можно сделать различными способами, например через портал hello, T-SQL и API-интерфейс REST.</span><span class="sxs-lookup"><span data-stu-id="f75de-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="f75de-195">Как масштабировать вычислительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f75de-195">How do I scale compute?</span></span>
<span data-ttu-id="f75de-196">Вычислительной мощности осуществляется хранилище данных SQL путем изменения параметра DWU hello.</span><span class="sxs-lookup"><span data-stu-id="f75de-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="f75de-197">При добавлении дополнительных DWU для некоторых операций производительность будет повышаться [линейно][linearly].</span><span class="sxs-lookup"><span data-stu-id="f75de-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="f75de-198">Мы разработали предложения DWU, благодаря которым ваша производительность заметно изменится при уменьшении или увеличении масштаба системы.</span><span class="sxs-lookup"><span data-stu-id="f75de-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="f75de-199">tooadjust Dwu, можно использовать любой из этих отдельных методов.</span><span class="sxs-lookup"><span data-stu-id="f75de-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="f75de-200">[Масштабирование вычислительных ресурсов с помощью портала Azure][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f75de-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="f75de-201">[Масштабирование вычислительных ресурсов с помощью PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f75de-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="f75de-202">[Масштабирование вычислительных ресурсов с помощью REST API][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f75de-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="f75de-203">[Масштабирование вычислительных ресурсов с помощью TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="f75de-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="f75de-204">Сколько DWU нужно использовать</span><span class="sxs-lookup"><span data-stu-id="f75de-204">How many DWUs should I use?</span></span>

<span data-ttu-id="f75de-205">toounderstand является какие вашей оптимальное значение DWU, попробуйте масштабирование вверх и вниз, а запустить несколько запросов после загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="f75de-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="f75de-206">Так как масштабирование выполняется достаточно быстро, попробуйте использовать разные уровни производительности не дольше одного часа.</span><span class="sxs-lookup"><span data-stu-id="f75de-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="f75de-207">Хранилище данных SQL — спроектированный tooprocess больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="f75de-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="f75de-208">toosee истинные возможности масштабирования, особенно в больших Dwu требуется toouse большой набор данных, который достигает или превышает 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="f75de-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="f75de-209">Рекомендации при поиске hello наиболее DWU для рабочей нагрузки:</span><span class="sxs-lookup"><span data-stu-id="f75de-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="f75de-210">Если хранилище данных только создается, начните с небольшого уровня производительности, обеспечиваемого DWU.</span><span class="sxs-lookup"><span data-stu-id="f75de-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="f75de-211">В качестве отправной точки можно использовать DW400 или DW200.</span><span class="sxs-lookup"><span data-stu-id="f75de-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="f75de-212">Отслеживать производительность приложений, наблюдая hello число выбранных Dwu по сравнению toohello производительности, которые вы заметили.</span><span class="sxs-lookup"><span data-stu-id="f75de-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="f75de-213">Определяет, насколько снизится производительность быстрее или медленнее, должна быть вы tooreach hello оптимальный уровень производительности требований, предполагая, что линейной шкалы.</span><span class="sxs-lookup"><span data-stu-id="f75de-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="f75de-214">Увеличьте или уменьшите число hello Dwu в toohow пропорции гораздо быстрее или медленнее, которую должна tooperform вашей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f75de-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="f75de-215">Вносите изменения, пока не достигнете уровня производительности, который оптимально отвечает вашим бизнес-требованиям.</span><span class="sxs-lookup"><span data-stu-id="f75de-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="f75de-216">Производительность запросов увеличивается только с дополнительные параллелизации, если hello работы могут быть разделены вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="f75de-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="f75de-217">Если обнаружится, что масштабирование не меняет его производительности, проверьте out наши статьи toocheck ли ваш данные распределяются неравномерно или представили большой объем перемещения данных с настройкой производительности.</span><span class="sxs-lookup"><span data-stu-id="f75de-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="f75de-218">Когда следует масштабировать DWU</span><span class="sxs-lookup"><span data-stu-id="f75de-218">When should I scale DWUs?</span></span>
<span data-ttu-id="f75de-219">Масштабирование Dwu изменяет hello следующие обстоятельства:</span><span class="sxs-lookup"><span data-stu-id="f75de-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="f75de-220">Линейно изменения производительности системы hello для сканирования, статистические выражения и операторы CTAS</span><span class="sxs-lookup"><span data-stu-id="f75de-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="f75de-221">При увеличении числа hello средств чтения и записи при загрузке с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="f75de-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="f75de-222">Максимальное количество параллельных запросов и слотов выдачи.</span><span class="sxs-lookup"><span data-stu-id="f75de-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="f75de-223">Рекомендации по tooscale Dwu:</span><span class="sxs-lookup"><span data-stu-id="f75de-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="f75de-224">Прежде чем выполнять ресурсоемкую загрузку данных или их преобразование, увеличьте объем DWU, чтобы быстрее получать доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="f75de-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="f75de-225">Рабочее время масштабируйте tooaccommodate большое количество параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="f75de-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="f75de-226">Приостановка работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="f75de-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="f75de-227">toopause базы данных, используйте любой из этих отдельные методы.</span><span class="sxs-lookup"><span data-stu-id="f75de-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="f75de-228">[Приостановка работы вычислительных ресурсов с помощью портала Azure][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f75de-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="f75de-229">[Приостановка работы вычислительных ресурсов с помощью PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f75de-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="f75de-230">[Приостановка работы вычислительных ресурсов с помощью REST API][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f75de-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="f75de-231">Возобновление работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="f75de-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="f75de-232">tooresume базы данных, используйте любой из этих отдельные методы.</span><span class="sxs-lookup"><span data-stu-id="f75de-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="f75de-233">[Возобновление работы вычислительных ресурсов с помощью портала Azure][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="f75de-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="f75de-234">[Возобновление работы вычислительных ресурсов с помощью PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f75de-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="f75de-235">[Возобновление работы вычислительных ресурсов с помощью REST API][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f75de-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="f75de-236">Проверка состояния базы данных</span><span class="sxs-lookup"><span data-stu-id="f75de-236">Check database state</span></span> 

<span data-ttu-id="f75de-237">tooresume базы данных, используйте любой из этих отдельные методы.</span><span class="sxs-lookup"><span data-stu-id="f75de-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="f75de-238">[проверка состояния базы данных с помощью T-SQL;][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="f75de-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="f75de-239">[проверка состояния базы данных с помощью PowerShell;][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="f75de-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="f75de-240">[проверка состояния базы данных с помощью REST API.][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="f75de-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="f75de-241">Разрешения</span><span class="sxs-lookup"><span data-stu-id="f75de-241">Permissions</span></span>

<span data-ttu-id="f75de-242">Масштабирования hello база данных требует hello разрешениями, описанными в [инструкции ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="f75de-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="f75de-243">Приостановка и возобновление требуют hello [участника базы данных SQL] [ SQL DB Contributor] разрешение, в частности Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="f75de-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="f75de-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f75de-244">Next steps</span></span>
<span data-ttu-id="f75de-245">См. следующие статьи toohelp вы понимаете такие концепции некоторые дополнительные производительности toohello:</span><span class="sxs-lookup"><span data-stu-id="f75de-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="f75de-246">[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="f75de-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="f75de-247">[Общие сведения о таблицах в хранилище данных SQL][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="f75de-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="f75de-248">[Распределение таблиц в хранилище данных SQL][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="f75de-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="f75de-249">[Indexing tables in SQL Data Warehouse (Индексирование таблиц в хранилище данных SQL)][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="f75de-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="f75de-250">[Секционирование таблиц в хранилище данных SQL][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="f75de-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="f75de-251">[Управление статистикой таблиц в хранилище данных SQL][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="f75de-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="f75de-252">[Рекомендации по использованию хранилища данных SQL Azure][Best practices]</span><span class="sxs-lookup"><span data-stu-id="f75de-252">[Best practices][Best practices]</span></span>

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
