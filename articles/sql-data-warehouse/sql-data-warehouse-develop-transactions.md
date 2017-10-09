---
title: "aaaTransactions в хранилище данных SQL | Документы Microsoft"
description: "Советы по реализации транзакций Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="6b6aa-103">Транзакции в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="6b6aa-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="6b6aa-104">Как и следовало ожидать, хранилище данных SQL поддерживает транзакции, как часть загрузки хранилища данных hello.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="6b6aa-105">Однако tooensure hello производительности хранилища данных SQL поддерживается в масштабе, некоторые функции будут ограничены при сравниваемых tooSQL сервера.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="6b6aa-106">В этой статье указаны различия hello и списки hello другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="6b6aa-107">Уровни изоляции транзакций</span><span class="sxs-lookup"><span data-stu-id="6b6aa-107">Transaction isolation levels</span></span>
<span data-ttu-id="6b6aa-108">Хранилище данных SQL реализует транзакции ACID.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="6b6aa-109">Однако hello изоляции транзакций поддержки hello ограничено слишком`READ UNCOMMITTED` и его изменить нельзя.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="6b6aa-110">Можно реализовать несколько методов кодирования, которые считывает tooprevent "грязных" данных, в случае серьезной проблемой.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="6b6aa-111">Hello наиболее популярных методов использовать как CTAS и переключения секций таблицы (часто называемом hello шаблон скользящего окна) пользователям tooprevent выполнение запросов к данным по-прежнему идет подготовка.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="6b6aa-112">Представления hello предварительную фильтрацию данных также является популярным подходом.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="6b6aa-113">Размер транзакции</span><span class="sxs-lookup"><span data-stu-id="6b6aa-113">Transaction size</span></span>
<span data-ttu-id="6b6aa-114">Размер одной транзакции, изменяющей данные, ограничен.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="6b6aa-115">ограничение Hello сегодня применяется «по распространения».</span><span class="sxs-lookup"><span data-stu-id="6b6aa-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="6b6aa-116">Таким образом можно вычислить общее выделение hello путем умножения hello ограничение на число распределения hello.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="6b6aa-117">tooapproximate hello максимальное число строк в транзакции hello разделите cap распространения hello hello общий размер каждой строки.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="6b6aa-118">Для столбцов переменной длины, рассмотрите возможность создания является длина столбца среднее, а не с помощью hello максимальный размер.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="6b6aa-119">Hello таблицы ниже hello были сделаны следующие допущения:</span><span class="sxs-lookup"><span data-stu-id="6b6aa-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="6b6aa-120">выполнено равномерное распределение данных;</span><span class="sxs-lookup"><span data-stu-id="6b6aa-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="6b6aa-121">Hello Средняя длина строки составляет 250 байт</span><span class="sxs-lookup"><span data-stu-id="6b6aa-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="6b6aa-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="6b6aa-122">[DWU][DWU]</span></span> | <span data-ttu-id="6b6aa-123">Ограничение распределения (ГиБ)</span><span class="sxs-lookup"><span data-stu-id="6b6aa-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="6b6aa-124">Число распределений</span><span class="sxs-lookup"><span data-stu-id="6b6aa-124">Number of Distributions</span></span> | <span data-ttu-id="6b6aa-125">Максимальный размер транзакции (ГиБ)</span><span class="sxs-lookup"><span data-stu-id="6b6aa-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="6b6aa-126"># Строк на распространения</span><span class="sxs-lookup"><span data-stu-id="6b6aa-126"># Rows per distribution</span></span> | <span data-ttu-id="6b6aa-127">Максимальное число строк на транзакцию</span><span class="sxs-lookup"><span data-stu-id="6b6aa-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6b6aa-128">DW100</span><span class="sxs-lookup"><span data-stu-id="6b6aa-128">DW100</span></span> |<span data-ttu-id="6b6aa-129">1</span><span class="sxs-lookup"><span data-stu-id="6b6aa-129">1</span></span> |<span data-ttu-id="6b6aa-130">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-130">60</span></span> |<span data-ttu-id="6b6aa-131">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-131">60</span></span> |<span data-ttu-id="6b6aa-132">4 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-132">4,000,000</span></span> |<span data-ttu-id="6b6aa-133">240 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-133">240,000,000</span></span> |
| <span data-ttu-id="6b6aa-134">DW200</span><span class="sxs-lookup"><span data-stu-id="6b6aa-134">DW200</span></span> |<span data-ttu-id="6b6aa-135">1.5</span><span class="sxs-lookup"><span data-stu-id="6b6aa-135">1.5</span></span> |<span data-ttu-id="6b6aa-136">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-136">60</span></span> |<span data-ttu-id="6b6aa-137">90</span><span class="sxs-lookup"><span data-stu-id="6b6aa-137">90</span></span> |<span data-ttu-id="6b6aa-138">6 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-138">6,000,000</span></span> |<span data-ttu-id="6b6aa-139">360 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-139">360,000,000</span></span> |
| <span data-ttu-id="6b6aa-140">DW300</span><span class="sxs-lookup"><span data-stu-id="6b6aa-140">DW300</span></span> |<span data-ttu-id="6b6aa-141">2.25</span><span class="sxs-lookup"><span data-stu-id="6b6aa-141">2.25</span></span> |<span data-ttu-id="6b6aa-142">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-142">60</span></span> |<span data-ttu-id="6b6aa-143">135</span><span class="sxs-lookup"><span data-stu-id="6b6aa-143">135</span></span> |<span data-ttu-id="6b6aa-144">9 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-144">9,000,000</span></span> |<span data-ttu-id="6b6aa-145">540 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-145">540,000,000</span></span> |
| <span data-ttu-id="6b6aa-146">DW400</span><span class="sxs-lookup"><span data-stu-id="6b6aa-146">DW400</span></span> |<span data-ttu-id="6b6aa-147">3</span><span class="sxs-lookup"><span data-stu-id="6b6aa-147">3</span></span> |<span data-ttu-id="6b6aa-148">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-148">60</span></span> |<span data-ttu-id="6b6aa-149">180</span><span class="sxs-lookup"><span data-stu-id="6b6aa-149">180</span></span> |<span data-ttu-id="6b6aa-150">12 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-150">12,000,000</span></span> |<span data-ttu-id="6b6aa-151">720 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-151">720,000,000</span></span> |
| <span data-ttu-id="6b6aa-152">DW500</span><span class="sxs-lookup"><span data-stu-id="6b6aa-152">DW500</span></span> |<span data-ttu-id="6b6aa-153">3,75</span><span class="sxs-lookup"><span data-stu-id="6b6aa-153">3.75</span></span> |<span data-ttu-id="6b6aa-154">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-154">60</span></span> |<span data-ttu-id="6b6aa-155">225</span><span class="sxs-lookup"><span data-stu-id="6b6aa-155">225</span></span> |<span data-ttu-id="6b6aa-156">15 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-156">15,000,000</span></span> |<span data-ttu-id="6b6aa-157">900 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-157">900,000,000</span></span> |
| <span data-ttu-id="6b6aa-158">DW600</span><span class="sxs-lookup"><span data-stu-id="6b6aa-158">DW600</span></span> |<span data-ttu-id="6b6aa-159">4.5.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-159">4.5</span></span> |<span data-ttu-id="6b6aa-160">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-160">60</span></span> |<span data-ttu-id="6b6aa-161">270</span><span class="sxs-lookup"><span data-stu-id="6b6aa-161">270</span></span> |<span data-ttu-id="6b6aa-162">18 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-162">18,000,000</span></span> |<span data-ttu-id="6b6aa-163">1 080 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-163">1,080,000,000</span></span> |
| <span data-ttu-id="6b6aa-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-164">DW1000</span></span> |<span data-ttu-id="6b6aa-165">7.5</span><span class="sxs-lookup"><span data-stu-id="6b6aa-165">7.5</span></span> |<span data-ttu-id="6b6aa-166">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-166">60</span></span> |<span data-ttu-id="6b6aa-167">450</span><span class="sxs-lookup"><span data-stu-id="6b6aa-167">450</span></span> |<span data-ttu-id="6b6aa-168">30 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-168">30,000,000</span></span> |<span data-ttu-id="6b6aa-169">1 800 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-169">1,800,000,000</span></span> |
| <span data-ttu-id="6b6aa-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="6b6aa-170">DW1200</span></span> |<span data-ttu-id="6b6aa-171">9</span><span class="sxs-lookup"><span data-stu-id="6b6aa-171">9</span></span> |<span data-ttu-id="6b6aa-172">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-172">60</span></span> |<span data-ttu-id="6b6aa-173">540</span><span class="sxs-lookup"><span data-stu-id="6b6aa-173">540</span></span> |<span data-ttu-id="6b6aa-174">36 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-174">36,000,000</span></span> |<span data-ttu-id="6b6aa-175">2 160 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-175">2,160,000,000</span></span> |
| <span data-ttu-id="6b6aa-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="6b6aa-176">DW1500</span></span> |<span data-ttu-id="6b6aa-177">11,25</span><span class="sxs-lookup"><span data-stu-id="6b6aa-177">11.25</span></span> |<span data-ttu-id="6b6aa-178">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-178">60</span></span> |<span data-ttu-id="6b6aa-179">675</span><span class="sxs-lookup"><span data-stu-id="6b6aa-179">675</span></span> |<span data-ttu-id="6b6aa-180">45 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-180">45,000,000</span></span> |<span data-ttu-id="6b6aa-181">2 700 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-181">2,700,000,000</span></span> |
| <span data-ttu-id="6b6aa-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-182">DW2000</span></span> |<span data-ttu-id="6b6aa-183">15</span><span class="sxs-lookup"><span data-stu-id="6b6aa-183">15</span></span> |<span data-ttu-id="6b6aa-184">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-184">60</span></span> |<span data-ttu-id="6b6aa-185">900</span><span class="sxs-lookup"><span data-stu-id="6b6aa-185">900</span></span> |<span data-ttu-id="6b6aa-186">60 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-186">60,000,000</span></span> |<span data-ttu-id="6b6aa-187">3 600 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-187">3,600,000,000</span></span> |
| <span data-ttu-id="6b6aa-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-188">DW3000</span></span> |<span data-ttu-id="6b6aa-189">22,5</span><span class="sxs-lookup"><span data-stu-id="6b6aa-189">22.5</span></span> |<span data-ttu-id="6b6aa-190">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-190">60</span></span> |<span data-ttu-id="6b6aa-191">1350</span><span class="sxs-lookup"><span data-stu-id="6b6aa-191">1,350</span></span> |<span data-ttu-id="6b6aa-192">90 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-192">90,000,000</span></span> |<span data-ttu-id="6b6aa-193">5 400 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-193">5,400,000,000</span></span> |
| <span data-ttu-id="6b6aa-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-194">DW6000</span></span> |<span data-ttu-id="6b6aa-195">45</span><span class="sxs-lookup"><span data-stu-id="6b6aa-195">45</span></span> |<span data-ttu-id="6b6aa-196">60</span><span class="sxs-lookup"><span data-stu-id="6b6aa-196">60</span></span> |<span data-ttu-id="6b6aa-197">2700</span><span class="sxs-lookup"><span data-stu-id="6b6aa-197">2,700</span></span> |<span data-ttu-id="6b6aa-198">180 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-198">180,000,000</span></span> |<span data-ttu-id="6b6aa-199">10 800 000 000</span><span class="sxs-lookup"><span data-stu-id="6b6aa-199">10,800,000,000</span></span> |

<span data-ttu-id="6b6aa-200">Ограничение размера транзакции Hello применяется по операции или операции.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="6b6aa-201">Оно не применяется к совокупности параллельных транзакций.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="6b6aa-202">Поэтому каждая транзакция не допускается toowrite такой объем данных журнала toohello.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="6b6aa-203">toooptimize и свести к минимуму объем hello данные, записанные в журнал toohello можно найти toohello [транзакций рекомендации] [ Transactions best practices] статьи.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="6b6aa-204">Максимальный размер транзакций могут быть осуществлены только для ХЭШИРОВАНИЯ или ROUND_ROBIN распределенных таблиц, где распространяться hello hello данных Hello является четным.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="6b6aa-205">Если hello транзакции записывает данные в виде асимметричные toohello распределения затем hello ограничен скорее всего toobe достигла размера предыдущих toohello максимальное транзакции.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="6b6aa-206">Состояние транзакции</span><span class="sxs-lookup"><span data-stu-id="6b6aa-206">Transaction state</span></span>
<span data-ttu-id="6b6aa-207">Хранилище данных SQL использует tooreport функции hello XACT_STATE() поврежденную транзакцию, используя hello значение -2.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="6b6aa-208">Это означает, что транзакции hello произошел сбой и помечен только для отката</span><span class="sxs-lookup"><span data-stu-id="6b6aa-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="6b6aa-209">Hello использовать-2, toodenote Функция XACT_STATE hello tooSQL другое поведение представляет поврежденную транзакцию сервера.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="6b6aa-210">SQL Server использует значение -1 hello toorepresent нефиксируемой транзакции.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="6b6aa-211">SQL Server может выдержать некоторые ошибки внутри транзакции без обращения toobe помечен как нефиксируемой.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="6b6aa-212">Например, `SELECT 1/0` вызовет ошибку, но не приведет к переходу транзакции в состояние нефиксируемой.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="6b6aa-213">SQL Server также позволяет считывает hello нефиксируемой транзакции.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="6b6aa-214">Тем не менее хранилище данных SQL не позволяет это сделать.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="6b6aa-215">При возникновении ошибки в ходе транзакции, хранилище данных SQL автоматически перейдет в состояние hello -2 и не будет возможности toomake любые дополнительные инструкции select пока не будет выполнен откат инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="6b6aa-216">Вот почему важно toocheck, что toosee код вашего приложения, если она использует XACT_STATE(), что вы может потребовать изменения в код toomake.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="6b6aa-217">Например, в SQL Server можно увидеть транзакцию следующего вида.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="6b6aa-218">Если оставить код как выше вы получите hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="6b6aa-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="6b6aa-219">Msg 111233, уровень 16, состояние 1, строка 1 111233; hello текущих транзакция была прервана, и все ожидающие изменения, был выполнен откат.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="6b6aa-220">Причина: для транзакции в состоянии "только откат" не был выполнен явный откат перед инструкцией DDL, DML или SELECT.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="6b6aa-221">Также не будет hello вывода hello ошибку_ * функций.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="6b6aa-222">В хранилище данных SQL кода hello должно toobe немного изменены:</span><span class="sxs-lookup"><span data-stu-id="6b6aa-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="6b6aa-223">Hello ожидается, что теперь соблюдается режим работы.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="6b6aa-224">Ошибка Hello в транзакции hello осуществляется и hello ошибку_ * функции предоставляют значения, как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="6b6aa-225">Все, что изменилось — что hello `ROLLBACK` из hello транзакции имела toohappen до чтения hello hello сведения об ошибках в hello `CATCH` блока.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="6b6aa-226">Функция Error_Line()</span><span class="sxs-lookup"><span data-stu-id="6b6aa-226">Error_Line() function</span></span>
<span data-ttu-id="6b6aa-227">Это также Обратите внимание, хранилище данных SQL не реализации поддержки функция ERROR_LINE() hello.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="6b6aa-228">Если у вас есть это в коде необходимо будет tooremove его toobe, совместимый с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="6b6aa-229">Вместо этого используйте запрос метки в коде tooimplement эквивалентную функциональность.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="6b6aa-230">См. toohello [МЕТКА] [ LABEL] Дополнительные сведения о данной функции.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="6b6aa-231">Использование THROW и RAISERROR</span><span class="sxs-lookup"><span data-stu-id="6b6aa-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="6b6aa-232">THROW — hello более современные реализацию для вызова исключения в хранилище данных SQL, но также поддерживается RAISERROR.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="6b6aa-233">Существует несколько различий, которые стоит рассмотреть обращая внимания toohowever.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="6b6aa-234">Определяемые пользователем сообщения об ошибках номера не может быть в hello 150 000 100 000 диапазона для THROW</span><span class="sxs-lookup"><span data-stu-id="6b6aa-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="6b6aa-235">Номера сообщений об ошибках RAISERROR не должны превышать 50 000.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="6b6aa-236">Не поддерживается использование sys.messages.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="6b6aa-237">Ограничения</span><span class="sxs-lookup"><span data-stu-id="6b6aa-237">Limitiations</span></span>
<span data-ttu-id="6b6aa-238">Хранилище данных SQL имеет несколько ограничений, которые связаны tootransactions.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="6b6aa-239">Вот они:</span><span class="sxs-lookup"><span data-stu-id="6b6aa-239">They are as follows:</span></span>

* <span data-ttu-id="6b6aa-240">не поддерживаются распределенные транзакции;</span><span class="sxs-lookup"><span data-stu-id="6b6aa-240">No distributed transactions</span></span>
* <span data-ttu-id="6b6aa-241">вложенные транзакции не разрешены;</span><span class="sxs-lookup"><span data-stu-id="6b6aa-241">No nested transactions permitted</span></span>
* <span data-ttu-id="6b6aa-242">не допускается точки сохранения.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-242">No save points allowed</span></span>
* <span data-ttu-id="6b6aa-243">не допускаются именованные транзакции;</span><span class="sxs-lookup"><span data-stu-id="6b6aa-243">No named transactions</span></span>
* <span data-ttu-id="6b6aa-244">не допускаются помеченные транзакции;</span><span class="sxs-lookup"><span data-stu-id="6b6aa-244">No marked transactions</span></span>
* <span data-ttu-id="6b6aa-245">не поддерживаются операторы DDL, такие как `CREATE TABLE` , внутри определенной пользователем транзакции.</span><span class="sxs-lookup"><span data-stu-id="6b6aa-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b6aa-246">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b6aa-246">Next steps</span></span>
<span data-ttu-id="6b6aa-247">toolearn более об оптимизации операций, в разделе [транзакций рекомендации][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="6b6aa-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="6b6aa-248">toolearn другие хранилища данных SQL советы и рекомендации, в разделе [рекомендации по хранилищу данных SQL][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="6b6aa-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
