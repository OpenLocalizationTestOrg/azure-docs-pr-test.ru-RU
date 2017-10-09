---
title: "Пакетная обработка производительность приложений баз данных SQL Azure tooimprove toouse aaaHow"
description: "Hello раздел предоставляет свидетельство, пакетная обработка операций базы данных значительно imroves hello скорости и масштабируемости приложений базы данных SQL Azure. Несмотря на то, что эти методы пакетной обработки работать для любой базы данных SQL Server, hello hello статьи занимается Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="700f2-104">Как toouse пакетной обработки tooimprove производительность приложения базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="700f2-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="700f2-105">Пакетная обработка операций tooAzure базы данных SQL значительно повышает hello производительности и масштабируемости приложений.</span><span class="sxs-lookup"><span data-stu-id="700f2-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="700f2-106">В порядке toounderstand hello преимуществ hello первой части этой статьи рассматриваются некоторые образцы результатов теста, которые сравнивают tooa последовательные и пакетные запросы базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="700f2-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="700f2-107">Hello оставшейся части статьи hello показаны методы hello, сценарии и рекомендации toohelp toouse успешно пакетной обработки в приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="700f2-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="700f2-108">Почему пакетная обработка так важна при работе с базой данных SQL</span><span class="sxs-lookup"><span data-stu-id="700f2-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="700f2-109">Пакетная обработка вызовов tooa удаленной службе является известной стратегией для повышения производительности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="700f2-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="700f2-110">Предусмотрены фиксированные обработки затраты tooany взаимодействия с удаленной службой, например сериализации и десериализации передача по сети.</span><span class="sxs-lookup"><span data-stu-id="700f2-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="700f2-111">Упаковка нескольких отдельных транзакций в один пакет позволяет сократить эти затраты.</span><span class="sxs-lookup"><span data-stu-id="700f2-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="700f2-112">В этом документе мы хотим tooexamine различные стратегии пакетной обработки базы данных SQL и сценариев.</span><span class="sxs-lookup"><span data-stu-id="700f2-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="700f2-113">Хотя эти стратегии также важны для локальных приложений, использующих SQL Server, существует несколько причин для выделения hello использованию пакетной обработки для базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="700f2-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="700f2-114">Потенциально большая задержка в сети в имеется доступ к базе данных SQL, особенно в том случае, если доступ к базе данных SQL из внешней hello одного центра обработки данных Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="700f2-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="700f2-115">Hello многопользовательских характеристики базы данных SQL означает, что hello эффективность hello данных доступ к toohello соотносится уровень масштабируемости hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="700f2-116">База данных SQL необходимо предотвратить монополизации базы данных ресурсов toohello ущерб другим клиентам любого одного клиента или пользователя.</span><span class="sxs-lookup"><span data-stu-id="700f2-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="700f2-117">В ответ toousage ресурсов сверх стандартных квот база данных SQL может уменьшить пропускную способность или реагировать в форме исключений регулирования.</span><span class="sxs-lookup"><span data-stu-id="700f2-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="700f2-118">Эффективные методы, такие как использование пакетирования, включите вы toodo больше работы в базе данных SQL до достижения этих ограничений.</span><span class="sxs-lookup"><span data-stu-id="700f2-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="700f2-119">Пакетная обработка также эффективна для архитектур, использующих несколько баз данных (сегментирование).</span><span class="sxs-lookup"><span data-stu-id="700f2-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="700f2-120">Hello эффективность взаимодействия с каждой единицы базы данных по-прежнему является ключевым фактором масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="700f2-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="700f2-121">Одним из hello преимущества использования базы данных SQL является отсутствие необходимости toomanage hello серверов, hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="700f2-122">Однако эта управляемая инфраструктура также означает наличие toothink по-разному об оптимизации базы данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="700f2-123">Больше не можно найти tooimprove hello инфраструктуры базы данных оборудования или сети.</span><span class="sxs-lookup"><span data-stu-id="700f2-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="700f2-124">Этими средами управляет Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="700f2-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="700f2-125">Hello главной области, которые можно контролировать — взаимодействие приложения с базой данных SQL.</span><span class="sxs-lookup"><span data-stu-id="700f2-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="700f2-126">Пакетная обработка выступает одним из методов такой оптимизации.</span><span class="sxs-lookup"><span data-stu-id="700f2-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="700f2-127">Первая часть Hello бумаги hello анализирует различные методы пакетной обработки для приложений .NET, использующих базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="700f2-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="700f2-128">последние два раздела Hello содержат пакетной обработки инструкции и сценарии.</span><span class="sxs-lookup"><span data-stu-id="700f2-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="700f2-129">Стратегии пакетной обработки</span><span class="sxs-lookup"><span data-stu-id="700f2-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="700f2-130">Примечание о результатах измерения времени в этом разделе</span><span class="sxs-lookup"><span data-stu-id="700f2-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="700f2-131">Результаты не являются тесты, но предназначены tooshow **относительную производительность**.</span><span class="sxs-lookup"><span data-stu-id="700f2-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="700f2-132">Временные показатели основаны на среднем значении результата выполнения минимум 10 тестов.</span><span class="sxs-lookup"><span data-stu-id="700f2-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="700f2-133">Операции представляют собой вставки в пустую таблицу.</span><span class="sxs-lookup"><span data-stu-id="700f2-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="700f2-134">Эти тесты были измеряемые предварительной версии 12, и они могут не соответствует toothroughput, могут возникнуть в версии 12 базы данных с помощью нового hello [уровней служб](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="700f2-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="700f2-135">относительное поощрение Hello hello метода пакетной обработки должна быть одинаковой.</span><span class="sxs-lookup"><span data-stu-id="700f2-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="700f2-136">Транзакции</span><span class="sxs-lookup"><span data-stu-id="700f2-136">Transactions</span></span>
<span data-ttu-id="700f2-137">Кажется странным toobegin рассмотрение пакетной обработки с обсуждения транзакций.</span><span class="sxs-lookup"><span data-stu-id="700f2-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="700f2-138">Но hello использование клиентских транзакций слабая пакетирования влияет серверные и улучшает производительность.</span><span class="sxs-lookup"><span data-stu-id="700f2-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="700f2-139">И транзакции можно добавлять только несколько строк кода, поэтому они обеспечивают быстрый способ tooimprove производительности последовательных операций.</span><span class="sxs-lookup"><span data-stu-id="700f2-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="700f2-140">Рассмотрим следующий код C#, который содержит последовательность вставки hello и обновления для простой таблицы.</span><span class="sxs-lookup"><span data-stu-id="700f2-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="700f2-141">Привет, выполнив кода ADO.NET последовательно выполняет эти операции.</span><span class="sxs-lookup"><span data-stu-id="700f2-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="700f2-142">Здравствуйте, лучшим способом toooptimize этот код является tooimplement некоторую форму клиентской пакетной обработки этих вызовов.</span><span class="sxs-lookup"><span data-stu-id="700f2-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="700f2-143">Но есть простой способ tooincrease hello производительность этот код просто обернуть последовательность вызовов hello в транзакции.</span><span class="sxs-lookup"><span data-stu-id="700f2-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="700f2-144">Вот hello того же кода, использующего транзакцию.</span><span class="sxs-lookup"><span data-stu-id="700f2-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="700f2-145">На самом деле, транзакции используются в обоих этих примерах.</span><span class="sxs-lookup"><span data-stu-id="700f2-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="700f2-146">В первом примере hello каждый отдельный вызов — это неявная транзакция.</span><span class="sxs-lookup"><span data-stu-id="700f2-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="700f2-147">В втором примере hello в явную транзакцию включаются все вызовы hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="700f2-148">В соответствии с документацией hello для hello [журнала транзакций с упреждающей записью](https://msdn.microsoft.com/library/ms186259.aspx), записей журнала, передан toohello диск при фиксации транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="700f2-149">Таким образом, включая больше вызовов в транзакцию, hello записи журнала транзакций toohello можно отложить до hello транзакция фиксируется.</span><span class="sxs-lookup"><span data-stu-id="700f2-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="700f2-150">В результате включается пакетной обработки для журнала транзакций hello записи toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="700f2-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="700f2-151">Hello в следующей таблице показаны некоторые результаты тестирования ad hoc.</span><span class="sxs-lookup"><span data-stu-id="700f2-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="700f2-152">выполнить тесты Hello приветствия же последовательные вставляет с и без транзакции.</span><span class="sxs-lookup"><span data-stu-id="700f2-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="700f2-153">Для разнообразия hello первый набор тестов удаленно запускался с ноутбука toohello базы данных в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="700f2-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="700f2-154">Hello второй набор тестов запускался из облачной службы и базы данных, которые размещались в hello же центре обработки данных Microsoft Azure (Запад США).</span><span class="sxs-lookup"><span data-stu-id="700f2-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="700f2-155">Hello следующей таблице показаны hello продолжительность в миллисекундах последовательных вставок с и без транзакции.</span><span class="sxs-lookup"><span data-stu-id="700f2-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="700f2-156">**В локальной среде tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="700f2-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="700f2-157">Операции</span><span class="sxs-lookup"><span data-stu-id="700f2-157">Operations</span></span> | <span data-ttu-id="700f2-158">Без транзакций (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-158">No Transaction (ms)</span></span> | <span data-ttu-id="700f2-159">С транзакциями (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="700f2-160">1</span><span class="sxs-lookup"><span data-stu-id="700f2-160">1</span></span> |<span data-ttu-id="700f2-161">130</span><span class="sxs-lookup"><span data-stu-id="700f2-161">130</span></span> |<span data-ttu-id="700f2-162">402</span><span class="sxs-lookup"><span data-stu-id="700f2-162">402</span></span> |
| <span data-ttu-id="700f2-163">10</span><span class="sxs-lookup"><span data-stu-id="700f2-163">10</span></span> |<span data-ttu-id="700f2-164">1208</span><span class="sxs-lookup"><span data-stu-id="700f2-164">1208</span></span> |<span data-ttu-id="700f2-165">1226</span><span class="sxs-lookup"><span data-stu-id="700f2-165">1226</span></span> |
| <span data-ttu-id="700f2-166">100</span><span class="sxs-lookup"><span data-stu-id="700f2-166">100</span></span> |<span data-ttu-id="700f2-167">12 662</span><span class="sxs-lookup"><span data-stu-id="700f2-167">12662</span></span> |<span data-ttu-id="700f2-168">10 395</span><span class="sxs-lookup"><span data-stu-id="700f2-168">10395</span></span> |
| <span data-ttu-id="700f2-169">1000</span><span class="sxs-lookup"><span data-stu-id="700f2-169">1000</span></span> |<span data-ttu-id="700f2-170">128 852</span><span class="sxs-lookup"><span data-stu-id="700f2-170">128852</span></span> |<span data-ttu-id="700f2-171">102 917</span><span class="sxs-lookup"><span data-stu-id="700f2-171">102917</span></span> |

<span data-ttu-id="700f2-172">**Azure tooAzure (одного центра обработки данных)**:</span><span class="sxs-lookup"><span data-stu-id="700f2-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="700f2-173">Операции</span><span class="sxs-lookup"><span data-stu-id="700f2-173">Operations</span></span> | <span data-ttu-id="700f2-174">Без транзакций (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-174">No Transaction (ms)</span></span> | <span data-ttu-id="700f2-175">С транзакциями (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="700f2-176">1</span><span class="sxs-lookup"><span data-stu-id="700f2-176">1</span></span> |<span data-ttu-id="700f2-177">21</span><span class="sxs-lookup"><span data-stu-id="700f2-177">21</span></span> |<span data-ttu-id="700f2-178">26</span><span class="sxs-lookup"><span data-stu-id="700f2-178">26</span></span> |
| <span data-ttu-id="700f2-179">10</span><span class="sxs-lookup"><span data-stu-id="700f2-179">10</span></span> |<span data-ttu-id="700f2-180">220</span><span class="sxs-lookup"><span data-stu-id="700f2-180">220</span></span> |<span data-ttu-id="700f2-181">56</span><span class="sxs-lookup"><span data-stu-id="700f2-181">56</span></span> |
| <span data-ttu-id="700f2-182">100</span><span class="sxs-lookup"><span data-stu-id="700f2-182">100</span></span> |<span data-ttu-id="700f2-183">2145</span><span class="sxs-lookup"><span data-stu-id="700f2-183">2145</span></span> |<span data-ttu-id="700f2-184">341</span><span class="sxs-lookup"><span data-stu-id="700f2-184">341</span></span> |
| <span data-ttu-id="700f2-185">1000</span><span class="sxs-lookup"><span data-stu-id="700f2-185">1000</span></span> |<span data-ttu-id="700f2-186">21 479</span><span class="sxs-lookup"><span data-stu-id="700f2-186">21479</span></span> |<span data-ttu-id="700f2-187">2756</span><span class="sxs-lookup"><span data-stu-id="700f2-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="700f2-188">Результаты не являются измерениями производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-188">Results are not benchmarks.</span></span> <span data-ttu-id="700f2-189">В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="700f2-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="700f2-190">На основе hello предыдущих результатов теста, фактически заключение одной операции в транзакции снижает производительность.</span><span class="sxs-lookup"><span data-stu-id="700f2-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="700f2-191">Однако по мере увеличения hello количества операций в рамках одной транзакции улучшение производительности hello становится более заметным.</span><span class="sxs-lookup"><span data-stu-id="700f2-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="700f2-192">Hello разницы в производительности также является наиболее заметно, когда все операции выполняются в центре обработки данных Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="700f2-193">Hello Повышенная задержка при использовании базы данных SQL из центра обработки данных Microsoft Azure вне hello неразборчивым hello рост производительности при использовании транзакций.</span><span class="sxs-lookup"><span data-stu-id="700f2-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="700f2-194">Хотя использование hello транзакций может увеличить производительность, по-прежнему слишком[рекомендации для транзакций, а соединения](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="700f2-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="700f2-195">Сохраните транзакции hello короткими hello возможные и закрыть подключение к базе данных после завершения работы hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="700f2-196">с помощью инструкции в предыдущем примере hello Hello гарантирует, что hello соединение закрывается, когда hello завершения последующего блока кода.</span><span class="sxs-lookup"><span data-stu-id="700f2-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="700f2-197">Hello предыдущем примере показано, что можно добавить код ADO.NET tooany локальной транзакции с двумя строками.</span><span class="sxs-lookup"><span data-stu-id="700f2-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="700f2-198">Транзакции обеспечивают быстрый способ производительность hello tooimprove кодом, который выполняет последовательные вставки, обновления и удаления операций.</span><span class="sxs-lookup"><span data-stu-id="700f2-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="700f2-199">Однако для hello наибольшую производительность, рассмотрите возможность изменения hello кода дальнейших tootake преимущества клиентской пакетной обработки, такие как параметры, возвращающие табличные значения.</span><span class="sxs-lookup"><span data-stu-id="700f2-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="700f2-200">Дополнительные сведения о транзакциях в ADO.NET см. в статье [Локальные транзакции](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="700f2-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="700f2-201">Параметры, которые возвращают табличное значение</span><span class="sxs-lookup"><span data-stu-id="700f2-201">Table-valued parameters</span></span>
<span data-ttu-id="700f2-202">Параметры, которые возвращают табличное значение, поддерживают определяемые пользователем типы таблиц в качестве параметров в инструкциях, хранимых процедурах и функциях Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="700f2-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="700f2-203">Этот метод пакетной обработки клиентского позволяет toosend несколько строк данных в рамках hello табличное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="700f2-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="700f2-204">toouse табличное значение параметров, необходимо сначала определить табличный тип.</span><span class="sxs-lookup"><span data-stu-id="700f2-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="700f2-205">Привет, следующем за инструкцией Transact-SQL создает табличный тип с именем **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="700f2-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="700f2-206">Создайте в коде **DataTable** с hello точного одинаковые имена и типы hello табличного типа.</span><span class="sxs-lookup"><span data-stu-id="700f2-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="700f2-207">Передайте этот экземпляр **DataTable** в качестве параметра в текстовом запросе или вызове хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="700f2-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="700f2-208">Hello ниже приведен пример этого метода.</span><span class="sxs-lookup"><span data-stu-id="700f2-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="700f2-209">В предыдущем примере hello hello **SqlCommand** объекта вставляет строки из параметров, возвращающих табличные значения,  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="700f2-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="700f2-210">ранее созданные Hello **DataTable** toothis параметр с hello присваивается объект **SqlCommand.Parameters.Add** метод.</span><span class="sxs-lookup"><span data-stu-id="700f2-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="700f2-211">Пакетная обработка операций вставки hello в одном вызова значительно повышает hello производительность через последовательные вставки.</span><span class="sxs-lookup"><span data-stu-id="700f2-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="700f2-212">tooimprove hello предыдущий пример еще больше, используйте хранимую процедуру вместо команды на основе текста.</span><span class="sxs-lookup"><span data-stu-id="700f2-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="700f2-213">Hello следующую команду Transact-SQL создает хранимую процедуру, которая принимает hello **SimpleTestTableType** табличное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="700f2-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="700f2-214">Затем измените hello **SqlCommand** объявления hello предыдущего кода примера toohello следующим объекта.</span><span class="sxs-lookup"><span data-stu-id="700f2-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="700f2-215">В большинстве случаев параметры, которые возвращают табличное значение, отличаются аналогичной или более высокой производительностью в сравнении с другими методами пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="700f2-216">Зачастую такие параметры более предпочтительны, так как они более универсальны в использовании, чем другие способы.</span><span class="sxs-lookup"><span data-stu-id="700f2-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="700f2-217">Например другие методы, такие как массовое копирование SQL, разрешите только hello вставки новых строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="700f2-218">Но и параметры, возвращающие табличные значения, можно использовать логику в toodetermine hello хранимые процедуры, какие строки являются обновления и которые являются вставляет.</span><span class="sxs-lookup"><span data-stu-id="700f2-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="700f2-219">Hello табличный тип также может быть toocontain измененный столбец «Операция», который показывает, определен ли hello строк следует вставить, обновить или удалить.</span><span class="sxs-lookup"><span data-stu-id="700f2-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="700f2-220">Hello в следующей таблице показаны результаты теста ad-hoc для hello использование возвращающих табличные значения параметров в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="700f2-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="700f2-221">Операции</span><span class="sxs-lookup"><span data-stu-id="700f2-221">Operations</span></span> | <span data-ttu-id="700f2-222">В локальной среде tooAzure (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="700f2-223">Один центр обработки данных Azure (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="700f2-224">1</span><span class="sxs-lookup"><span data-stu-id="700f2-224">1</span></span> |<span data-ttu-id="700f2-225">124</span><span class="sxs-lookup"><span data-stu-id="700f2-225">124</span></span> |<span data-ttu-id="700f2-226">32</span><span class="sxs-lookup"><span data-stu-id="700f2-226">32</span></span> |
| <span data-ttu-id="700f2-227">10</span><span class="sxs-lookup"><span data-stu-id="700f2-227">10</span></span> |<span data-ttu-id="700f2-228">131</span><span class="sxs-lookup"><span data-stu-id="700f2-228">131</span></span> |<span data-ttu-id="700f2-229">25</span><span class="sxs-lookup"><span data-stu-id="700f2-229">25</span></span> |
| <span data-ttu-id="700f2-230">100</span><span class="sxs-lookup"><span data-stu-id="700f2-230">100</span></span> |<span data-ttu-id="700f2-231">338</span><span class="sxs-lookup"><span data-stu-id="700f2-231">338</span></span> |<span data-ttu-id="700f2-232">51</span><span class="sxs-lookup"><span data-stu-id="700f2-232">51</span></span> |
| <span data-ttu-id="700f2-233">1000</span><span class="sxs-lookup"><span data-stu-id="700f2-233">1000</span></span> |<span data-ttu-id="700f2-234">2615</span><span class="sxs-lookup"><span data-stu-id="700f2-234">2615</span></span> |<span data-ttu-id="700f2-235">382</span><span class="sxs-lookup"><span data-stu-id="700f2-235">382</span></span> |
| <span data-ttu-id="700f2-236">10 000</span><span class="sxs-lookup"><span data-stu-id="700f2-236">10000</span></span> |<span data-ttu-id="700f2-237">23 830</span><span class="sxs-lookup"><span data-stu-id="700f2-237">23830</span></span> |<span data-ttu-id="700f2-238">3586</span><span class="sxs-lookup"><span data-stu-id="700f2-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="700f2-239">Результаты не являются измерениями производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-239">Results are not benchmarks.</span></span> <span data-ttu-id="700f2-240">В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="700f2-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="700f2-241">Hello выигрыш в производительности благодаря пакетной обработке заметно сразу.</span><span class="sxs-lookup"><span data-stu-id="700f2-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="700f2-242">В hello предыдущем последовательном тесте 1000 операций выполнялись 129 секунд вне hello центра обработки данных и 21 секунду в центре обработки данных hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="700f2-243">Однако с помощью параметров, возвращающих табличные значения, 1000 операций выполнялись только 2,6 секунды вне центра обработки данных hello и 0,4 секунды в центре обработки данных hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="700f2-244">Дополнительные сведения о параметрах с табличным значением см. в разделе [Параметры, которые возвращают табличное значение](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="700f2-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="700f2-245">Массовое копирование SQL</span><span class="sxs-lookup"><span data-stu-id="700f2-245">SQL bulk copy</span></span>
<span data-ttu-id="700f2-246">Массовое копирование SQL является другим способом tooinsert больших объемов данных в целевую базу данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="700f2-247">Приложения .NET могут использовать hello **SqlBulkCopy** операции класс tooperform массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="700f2-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="700f2-248">**SqlBulkCopy** работает аналогично функции toohello командной строки, **Bcp.exe**, или hello инструкции Transact-SQL, **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="700f2-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="700f2-249">Hello следующем примере кода показано, как hello toobulk копирования строк в источнике hello **DataTable**, таблица, toohello целевая таблица в SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="700f2-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="700f2-250">В некоторых случаях вместо параметров, которые возвращают табличное значение, рекомендуется использовать массовое копирование.</span><span class="sxs-lookup"><span data-stu-id="700f2-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="700f2-251">См. таблицу сравнения hello возвращающих табличные значения параметров и операций МАССОВОЙ вставки в разделе hello [табличное значение параметры](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="700f2-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="700f2-252">Hello следующие ad-результаты теста показывают производительность пакетной обработки с hello **SqlBulkCopy** в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="700f2-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="700f2-253">Операции</span><span class="sxs-lookup"><span data-stu-id="700f2-253">Operations</span></span> | <span data-ttu-id="700f2-254">В локальной среде tooAzure (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="700f2-255">Один центр обработки данных Azure (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="700f2-256">1</span><span class="sxs-lookup"><span data-stu-id="700f2-256">1</span></span> |<span data-ttu-id="700f2-257">433</span><span class="sxs-lookup"><span data-stu-id="700f2-257">433</span></span> |<span data-ttu-id="700f2-258">57</span><span class="sxs-lookup"><span data-stu-id="700f2-258">57</span></span> |
| <span data-ttu-id="700f2-259">10</span><span class="sxs-lookup"><span data-stu-id="700f2-259">10</span></span> |<span data-ttu-id="700f2-260">441</span><span class="sxs-lookup"><span data-stu-id="700f2-260">441</span></span> |<span data-ttu-id="700f2-261">32</span><span class="sxs-lookup"><span data-stu-id="700f2-261">32</span></span> |
| <span data-ttu-id="700f2-262">100</span><span class="sxs-lookup"><span data-stu-id="700f2-262">100</span></span> |<span data-ttu-id="700f2-263">636</span><span class="sxs-lookup"><span data-stu-id="700f2-263">636</span></span> |<span data-ttu-id="700f2-264">53</span><span class="sxs-lookup"><span data-stu-id="700f2-264">53</span></span> |
| <span data-ttu-id="700f2-265">1000</span><span class="sxs-lookup"><span data-stu-id="700f2-265">1000</span></span> |<span data-ttu-id="700f2-266">2535</span><span class="sxs-lookup"><span data-stu-id="700f2-266">2535</span></span> |<span data-ttu-id="700f2-267">341</span><span class="sxs-lookup"><span data-stu-id="700f2-267">341</span></span> |
| <span data-ttu-id="700f2-268">10 000</span><span class="sxs-lookup"><span data-stu-id="700f2-268">10000</span></span> |<span data-ttu-id="700f2-269">21 605</span><span class="sxs-lookup"><span data-stu-id="700f2-269">21605</span></span> |<span data-ttu-id="700f2-270">2737</span><span class="sxs-lookup"><span data-stu-id="700f2-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="700f2-271">Результаты не являются измерениями производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-271">Results are not benchmarks.</span></span> <span data-ttu-id="700f2-272">В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="700f2-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="700f2-273">В пакетах меньшего размера, hello используют возвращающие табличные значения параметры превзошли hello **SqlBulkCopy** класса.</span><span class="sxs-lookup"><span data-stu-id="700f2-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="700f2-274">Тем не менее **SqlBulkCopy** выполнить 12-31% быстрее, чем табличное значение параметров для тестов hello 1000 и 10 000 строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="700f2-275">Возвращающие табличные значения параметров, таких как **SqlBulkCopy** будет хорошим вариантом для пакетных вставок, особенно по сравнению производительности toohello непакетном операций.</span><span class="sxs-lookup"><span data-stu-id="700f2-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="700f2-276">Дополнительные сведения о массовом копировании в ADO.NET см. в [этой статье](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="700f2-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="700f2-277">Многострочные параметризованные инструкции INSERT</span><span class="sxs-lookup"><span data-stu-id="700f2-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="700f2-278">Альтернатива небольшим пакетам — большой tooconstruct параметризованные инструкции INSERT, которая вставляет несколько строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="700f2-279">Этот метод продемонстрирован в следующем примере кода Hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="700f2-280">Этот пример предназначен основной принцип tooshow hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="700f2-281">Более реалистичном случае будет произведен цикл через строку hello необходимые сущности tooconstruct hello запроса и параметры команды hello одновременно.</span><span class="sxs-lookup"><span data-stu-id="700f2-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="700f2-282">Может быть не более 2100 параметров запроса, поэтому это ограничивает общее число строк, которые могут быть обработаны таким образом hello tooa всего.</span><span class="sxs-lookup"><span data-stu-id="700f2-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="700f2-283">Здравствуйте, следуя ad-hoc тестирование результатов Показать hello производительности этого типа инструкций вставки в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="700f2-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="700f2-284">Операции</span><span class="sxs-lookup"><span data-stu-id="700f2-284">Operations</span></span> | <span data-ttu-id="700f2-285">Параметры, которые возвращают табличное значение (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="700f2-286">Один оператор INSERT (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="700f2-287">1</span><span class="sxs-lookup"><span data-stu-id="700f2-287">1</span></span> |<span data-ttu-id="700f2-288">32</span><span class="sxs-lookup"><span data-stu-id="700f2-288">32</span></span> |<span data-ttu-id="700f2-289">20</span><span class="sxs-lookup"><span data-stu-id="700f2-289">20</span></span> |
| <span data-ttu-id="700f2-290">10</span><span class="sxs-lookup"><span data-stu-id="700f2-290">10</span></span> |<span data-ttu-id="700f2-291">30</span><span class="sxs-lookup"><span data-stu-id="700f2-291">30</span></span> |<span data-ttu-id="700f2-292">25</span><span class="sxs-lookup"><span data-stu-id="700f2-292">25</span></span> |
| <span data-ttu-id="700f2-293">100</span><span class="sxs-lookup"><span data-stu-id="700f2-293">100</span></span> |<span data-ttu-id="700f2-294">33</span><span class="sxs-lookup"><span data-stu-id="700f2-294">33</span></span> |<span data-ttu-id="700f2-295">51</span><span class="sxs-lookup"><span data-stu-id="700f2-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="700f2-296">Результаты не являются измерениями производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-296">Results are not benchmarks.</span></span> <span data-ttu-id="700f2-297">В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="700f2-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="700f2-298">Этот подход показывает чуть более высокие результаты по времени для пакетов, состоящих менее чем из 100 строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="700f2-299">Несмотря на то, что улучшения hello мал, этот метод является другой параметр, который может работать в конкретном приложении.</span><span class="sxs-lookup"><span data-stu-id="700f2-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="700f2-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="700f2-300">DataAdapter</span></span>
<span data-ttu-id="700f2-301">Hello **DataAdapter** класс позволяет toomodify **DataSet** а затем отправить hello изменения как операции INSERT, UPDATE и DELETE.</span><span class="sxs-lookup"><span data-stu-id="700f2-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="700f2-302">Если вы используете hello **DataAdapter** таким образом, важно toonote, отдельные вызовы выполняются для каждой определенной операции.</span><span class="sxs-lookup"><span data-stu-id="700f2-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="700f2-303">tooimprove производительность, используйте hello **UpdateBatchSize** свойство toohello число операций, которые должны быть объединены одновременно.</span><span class="sxs-lookup"><span data-stu-id="700f2-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="700f2-304">Дополнительные сведения см. в статье [Выполнение пакетных операций с помощью объектов DataAdapter (ADO.NET)](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="700f2-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="700f2-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="700f2-305">Entity framework</span></span>
<span data-ttu-id="700f2-306">В настоящее время платформа Entity Framework не поддерживает пакетную обработку.</span><span class="sxs-lookup"><span data-stu-id="700f2-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="700f2-307">Разные разработчики в сообществе hello предпринята toodemonstrate обходные пути, например переопределение hello **SaveChanges** метод.</span><span class="sxs-lookup"><span data-stu-id="700f2-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="700f2-308">Но hello решения обычно сложны и подогнаны toohello приложения и модели данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="700f2-309">проект codeplex Hello Entity Framework в настоящее время содержит страницу с обсуждением запроса этой функции.</span><span class="sxs-lookup"><span data-stu-id="700f2-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="700f2-310">tooview данного обсуждения см [заметки о встрече разработки — 2 августа 2012 г.](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="700f2-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="700f2-311">XML</span><span class="sxs-lookup"><span data-stu-id="700f2-311">XML</span></span>
<span data-ttu-id="700f2-312">Для полноты информации мы думаем, что он является важным tootalk о XML как стратегию пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="700f2-313">Тем не менее использование hello XML имеет не преимуществ по сравнению с другими методами зато обладает несколькими недостатками.</span><span class="sxs-lookup"><span data-stu-id="700f2-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="700f2-314">Hello подход является одинаковых tootable возвращающих табличные значения параметров, но XML-файл или строка передается tooa хранимые процедуры вместо пользовательской таблицы.</span><span class="sxs-lookup"><span data-stu-id="700f2-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="700f2-315">Hello хранимой процедуры выполняет синтаксический анализ команды hello hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="700f2-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="700f2-316">Есть несколько недостатков toothis подход:</span><span class="sxs-lookup"><span data-stu-id="700f2-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="700f2-317">Работа с содержимым XML может быть весьма трудоемкой и приводить к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="700f2-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="700f2-318">Hello синтаксического анализа XML в базе данных hello может сильно нагружать Процессор.</span><span class="sxs-lookup"><span data-stu-id="700f2-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="700f2-319">В большинстве случаев при использовании этого метода операции выполняются медленнее, чем при использовании параметров, которые возвращают табличное значение.</span><span class="sxs-lookup"><span data-stu-id="700f2-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="700f2-320">По этой причине не рекомендуется использовать hello XML для пакетных запросов.</span><span class="sxs-lookup"><span data-stu-id="700f2-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="700f2-321">Рекомендации по использованию пакетной обработки</span><span class="sxs-lookup"><span data-stu-id="700f2-321">Batching considerations</span></span>
<span data-ttu-id="700f2-322">Дополнительные рекомендации по использованию hello пакетной обработки в приложениях баз данных SQL Hello в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="700f2-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="700f2-323">Компромиссы</span><span class="sxs-lookup"><span data-stu-id="700f2-323">Tradeoffs</span></span>
<span data-ttu-id="700f2-324">В зависимости от архитектуры использование пакетной обработки предполагает некоторый компромисс между производительностью и устойчивостью приложения.</span><span class="sxs-lookup"><span data-stu-id="700f2-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="700f2-325">Например рассмотрим сценарий hello, когда ваша роль неожиданно выходит из строя.</span><span class="sxs-lookup"><span data-stu-id="700f2-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="700f2-326">При потере одной строки данных, влияние hello меньше, чем потеря большого пакета неотправленных строк влияние hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="700f2-327">Нет повышается риск при буферизации строк перед их отправкой toohello базы данных в заданном периоде времени.</span><span class="sxs-lookup"><span data-stu-id="700f2-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="700f2-328">Вследствие этого вычисление типа hello операций этого пакета.</span><span class="sxs-lookup"><span data-stu-id="700f2-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="700f2-329">Следовательно, с данными, которые менее критичны, можно использовать пакеты более интенсивно (большие пакеты и более продолжительные периоды времени).</span><span class="sxs-lookup"><span data-stu-id="700f2-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="700f2-330">Размер пакета</span><span class="sxs-lookup"><span data-stu-id="700f2-330">Batch size</span></span>
<span data-ttu-id="700f2-331">В наших тестах обычно не было не преимущества toobreaking больших пакетов на более мелкие части.</span><span class="sxs-lookup"><span data-stu-id="700f2-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="700f2-332">На самом деле такое деление часто приводит к меньшей производительности по сравнению с отправкой одного большого пакета.</span><span class="sxs-lookup"><span data-stu-id="700f2-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="700f2-333">Например рассмотрим сценарий, где требуется tooinsert 1000 строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="700f2-334">Hello следующей таблице показано время, затрачиваемое табличное значение параметров toouse tooinsert 1000 строк при делении на более мелкие.</span><span class="sxs-lookup"><span data-stu-id="700f2-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="700f2-335">Размер пакета</span><span class="sxs-lookup"><span data-stu-id="700f2-335">Batch size</span></span> | <span data-ttu-id="700f2-336">Количество итераций</span><span class="sxs-lookup"><span data-stu-id="700f2-336">Iterations</span></span> | <span data-ttu-id="700f2-337">Параметры, которые возвращают табличное значение (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="700f2-338">1000</span><span class="sxs-lookup"><span data-stu-id="700f2-338">1000</span></span> |<span data-ttu-id="700f2-339">1</span><span class="sxs-lookup"><span data-stu-id="700f2-339">1</span></span> |<span data-ttu-id="700f2-340">347</span><span class="sxs-lookup"><span data-stu-id="700f2-340">347</span></span> |
| <span data-ttu-id="700f2-341">500</span><span class="sxs-lookup"><span data-stu-id="700f2-341">500</span></span> |<span data-ttu-id="700f2-342">2</span><span class="sxs-lookup"><span data-stu-id="700f2-342">2</span></span> |<span data-ttu-id="700f2-343">355</span><span class="sxs-lookup"><span data-stu-id="700f2-343">355</span></span> |
| <span data-ttu-id="700f2-344">100</span><span class="sxs-lookup"><span data-stu-id="700f2-344">100</span></span> |<span data-ttu-id="700f2-345">10</span><span class="sxs-lookup"><span data-stu-id="700f2-345">10</span></span> |<span data-ttu-id="700f2-346">465</span><span class="sxs-lookup"><span data-stu-id="700f2-346">465</span></span> |
| <span data-ttu-id="700f2-347">50</span><span class="sxs-lookup"><span data-stu-id="700f2-347">50</span></span> |<span data-ttu-id="700f2-348">20</span><span class="sxs-lookup"><span data-stu-id="700f2-348">20</span></span> |<span data-ttu-id="700f2-349">630</span><span class="sxs-lookup"><span data-stu-id="700f2-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="700f2-350">Результаты не являются измерениями производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-350">Results are not benchmarks.</span></span> <span data-ttu-id="700f2-351">В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="700f2-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="700f2-352">Можно видеть, что hello Наилучшая производительность для 1000 строк toosubmit их все одновременно.</span><span class="sxs-lookup"><span data-stu-id="700f2-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="700f2-353">В других тестах (не показанных здесь) было toobreak прирост производительности пакета 10000 строк на 2 пакета 5000.</span><span class="sxs-lookup"><span data-stu-id="700f2-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="700f2-354">Но hello схема таблицы для этих тестов довольно прост, и вам следует провести, тесты в ваших данных и пакете размеры tooverify эти результаты.</span><span class="sxs-lookup"><span data-stu-id="700f2-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="700f2-355">Другой фактор tooconsider, что всего пакета hello становится слишком большой, базы данных SQL может регулировать и отклонить toocommit hello пакета.</span><span class="sxs-lookup"><span data-stu-id="700f2-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="700f2-356">Для получения наилучших результатов hello тест вашего toodetermine конкретного сценария, если имеется идеальный размер пакета.</span><span class="sxs-lookup"><span data-stu-id="700f2-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="700f2-357">Сделайте размер пакета hello можно настроить при быстро регулировать tooenable среды выполнения на основе производительности или ошибок.</span><span class="sxs-lookup"><span data-stu-id="700f2-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="700f2-358">Наконец Сбалансируйте размер hello hello пакета с hello риски, связанные с пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="700f2-359">Если есть временные ошибки или сбоя роли hello, проанализируйте последствия hello повторное выполнение операции hello или потери данных hello в пакете hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="700f2-360">Параллельная обработка</span><span class="sxs-lookup"><span data-stu-id="700f2-360">Parallel processing</span></span>
<span data-ttu-id="700f2-361">Если заняло hello путь уменьшения размера пакета hello, а применение рабочих hello tooexecute нескольких потоков?</span><span class="sxs-lookup"><span data-stu-id="700f2-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="700f2-362">Снова-таки, результаты наших тестов продемонстрировали, что несколько мелких многопоточных пакетов, как правило, обрабатываются хуже, чем один большой пакет.</span><span class="sxs-lookup"><span data-stu-id="700f2-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="700f2-363">Hello следующий тест пытается tooinsert 1000 строк в одной или нескольких параллельных пакетах.</span><span class="sxs-lookup"><span data-stu-id="700f2-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="700f2-364">Результаты этого теста демонстрируют, что передача нескольких параллельных пакетов снизила производительность.</span><span class="sxs-lookup"><span data-stu-id="700f2-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="700f2-365">Размер пакета [количество итераций]</span><span class="sxs-lookup"><span data-stu-id="700f2-365">Batch size [Iterations]</span></span> | <span data-ttu-id="700f2-366">Два потока (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-366">Two threads (ms)</span></span> | <span data-ttu-id="700f2-367">Четыре потока (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-367">Four threads (ms)</span></span> | <span data-ttu-id="700f2-368">Шесть потоков (мс)</span><span class="sxs-lookup"><span data-stu-id="700f2-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="700f2-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="700f2-369">1000 [1]</span></span> |<span data-ttu-id="700f2-370">277</span><span class="sxs-lookup"><span data-stu-id="700f2-370">277</span></span> |<span data-ttu-id="700f2-371">315</span><span class="sxs-lookup"><span data-stu-id="700f2-371">315</span></span> |<span data-ttu-id="700f2-372">266</span><span class="sxs-lookup"><span data-stu-id="700f2-372">266</span></span> |
| <span data-ttu-id="700f2-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="700f2-373">500 [2]</span></span> |<span data-ttu-id="700f2-374">548</span><span class="sxs-lookup"><span data-stu-id="700f2-374">548</span></span> |<span data-ttu-id="700f2-375">278</span><span class="sxs-lookup"><span data-stu-id="700f2-375">278</span></span> |<span data-ttu-id="700f2-376">256</span><span class="sxs-lookup"><span data-stu-id="700f2-376">256</span></span> |
| <span data-ttu-id="700f2-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="700f2-377">250 [4]</span></span> |<span data-ttu-id="700f2-378">405</span><span class="sxs-lookup"><span data-stu-id="700f2-378">405</span></span> |<span data-ttu-id="700f2-379">329</span><span class="sxs-lookup"><span data-stu-id="700f2-379">329</span></span> |<span data-ttu-id="700f2-380">265</span><span class="sxs-lookup"><span data-stu-id="700f2-380">265</span></span> |
| <span data-ttu-id="700f2-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="700f2-381">100 [10]</span></span> |<span data-ttu-id="700f2-382">488</span><span class="sxs-lookup"><span data-stu-id="700f2-382">488</span></span> |<span data-ttu-id="700f2-383">439</span><span class="sxs-lookup"><span data-stu-id="700f2-383">439</span></span> |<span data-ttu-id="700f2-384">391</span><span class="sxs-lookup"><span data-stu-id="700f2-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="700f2-385">Результаты не являются измерениями производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-385">Results are not benchmarks.</span></span> <span data-ttu-id="700f2-386">В разделе hello [примечание об результаты измерения времени в этом разделе](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="700f2-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="700f2-387">Существует несколько возможных причин hello снижение производительности из-за tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="700f2-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="700f2-388">Выполняется несколько одновременных вызовов сети вместо одного.</span><span class="sxs-lookup"><span data-stu-id="700f2-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="700f2-389">Выполнение нескольких операций с одной таблицей может привести к состязанию и блокировке.</span><span class="sxs-lookup"><span data-stu-id="700f2-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="700f2-390">Возникают издержки, связанные с многопоточностью.</span><span class="sxs-lookup"><span data-stu-id="700f2-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="700f2-391">Hello расходы на открытие нескольких подключений перевешивают hello выгоду от параллельной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="700f2-392">Если целевая различных таблиц или баз данных, это возможно toosee получить некоторые производительности с помощью этой стратегии.</span><span class="sxs-lookup"><span data-stu-id="700f2-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="700f2-393">Этот метод подходит для сегментирования баз данных или использования федераций.</span><span class="sxs-lookup"><span data-stu-id="700f2-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="700f2-394">Сегментирование использует несколько баз данных и базы данных tooeach маршруты различных данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="700f2-395">Если каждый небольшой пакет направляется tooa другую базу данных, затем выполнение операций hello в параллельном режиме может быть более эффективным.</span><span class="sxs-lookup"><span data-stu-id="700f2-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="700f2-396">Тем не менее прирост производительности hello не является достаточной toouse как hello основания для принятия решений сегментирование баз данных toouse в решении.</span><span class="sxs-lookup"><span data-stu-id="700f2-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="700f2-397">В некоторых проектах параллельное выполнение небольших пакетов может привести к повышению пропускной способности запросов в системе под нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="700f2-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="700f2-398">Таким образом несмотря на то, что это быстрее tooprocess один большой пакет, обработка нескольких пакетов в параллельном режиме может быть более эффективным.</span><span class="sxs-lookup"><span data-stu-id="700f2-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="700f2-399">При использовании параллельного выполнения, рассмотрите возможность управления hello максимальное число рабочих потоков.</span><span class="sxs-lookup"><span data-stu-id="700f2-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="700f2-400">Меньшее количество потоков может привести к меньшему количеству состязаний и более быстрому выполнению.</span><span class="sxs-lookup"><span data-stu-id="700f2-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="700f2-401">Кроме того Учтите hello дополнительную нагрузку это дает на hello целевую базу данных как в соединений и транзакций.</span><span class="sxs-lookup"><span data-stu-id="700f2-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="700f2-402">Связанные факторы производительности</span><span class="sxs-lookup"><span data-stu-id="700f2-402">Related performance factors</span></span>
<span data-ttu-id="700f2-403">Типичные рекомендации по производительности базы данных относятся и к пакетной обработке.</span><span class="sxs-lookup"><span data-stu-id="700f2-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="700f2-404">Например, производительность операций вставки снижается для таблиц с большим первичным ключом или несколькими некластеризованными индексами.</span><span class="sxs-lookup"><span data-stu-id="700f2-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="700f2-405">Если хранимая процедура табличное значение параметров, можно использовать команду hello **SET NOCOUNT ON** в начале процедуры hello hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="700f2-406">Эта инструкция Подавляет возврат hello hello счетчик строк влияет hello в процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="700f2-407">Однако в наших тестах hello использование **SET NOCOUNT ON** не оказывает никакого влияния или снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="700f2-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="700f2-408">Hello хранимая процедура для теста была простой: с одним **вставить** команду hello табличное значение параметра.</span><span class="sxs-lookup"><span data-stu-id="700f2-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="700f2-409">Возможно, эта инструкция просто больше подходит для более сложных хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="700f2-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="700f2-410">Но нельзя предполагать, что добавление **SET NOCOUNT ON** tooyour хранимой процедуре автоматически повысит производительность.</span><span class="sxs-lookup"><span data-stu-id="700f2-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="700f2-411">toounderstand Здравствуйте эффект, проверьте хранимую процедуру с и без hello **SET NOCOUNT ON** инструкции.</span><span class="sxs-lookup"><span data-stu-id="700f2-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="700f2-412">Сценарии пакетной обработки</span><span class="sxs-lookup"><span data-stu-id="700f2-412">Batching scenarios</span></span>
<span data-ttu-id="700f2-413">Hello ниже описано, как toouse табличное значение параметров в трех различных случаях.</span><span class="sxs-lookup"><span data-stu-id="700f2-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="700f2-414">первый сценарий Hello показывает пакетную обработку и буферизацию возможной совместной работе.</span><span class="sxs-lookup"><span data-stu-id="700f2-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="700f2-415">Второй сценарий Hello повышает производительность за счет выполнения операции с основными данными в одном вызове хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="700f2-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="700f2-416">Здравствуйте, последнем сценарии показано как toouse табличное значение параметров в операции «Вставки-обновления».</span><span class="sxs-lookup"><span data-stu-id="700f2-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="700f2-417">Буферизация</span><span class="sxs-lookup"><span data-stu-id="700f2-417">Buffering</span></span>
<span data-ttu-id="700f2-418">Хотя некоторые сценарии явно предполагают пакетную обработку, во многих других сценариях можно использовать преимущество отложенной пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="700f2-419">Тем не менее отложенная обработка также несет большой риск того, hello данные теряются в событии hello непредвиденный сбой.</span><span class="sxs-lookup"><span data-stu-id="700f2-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="700f2-420">Он является важным toounderstand этот риск и принимать во внимание последствия hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="700f2-421">Например рассмотрим веб-приложение, которое отслеживает историю навигации каждого пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="700f2-422">При каждом запросе страницы приложение hello может делать представление страницы базы данных вызова toorecord hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="700f2-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="700f2-423">Но более высокую производительность и масштабируемость может осуществляться через буферизации действий пользователей hello навигации и последующей отправки этой базы данных toohello данных в пакетах.</span><span class="sxs-lookup"><span data-stu-id="700f2-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="700f2-424">Вы можете активировать hello обновление базы данных по истечении определенного времени или размер буфера.</span><span class="sxs-lookup"><span data-stu-id="700f2-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="700f2-425">Например правило может указывать, что этот пакет hello должен обрабатываться через 20 секунд или когда буфер hello достигает 1000 элементов.</span><span class="sxs-lookup"><span data-stu-id="700f2-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="700f2-426">Hello следующий пример кода использует [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess буфер событий, вызванных классом наблюдения.</span><span class="sxs-lookup"><span data-stu-id="700f2-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="700f2-427">Когда hello заполнения буфера или истечет время ожидания, hello пакет пользовательских данных отправляется toohello базы данных с помощью параметров, возвращающих табличные значения.</span><span class="sxs-lookup"><span data-stu-id="700f2-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="700f2-428">Здравствуйте, приведенные ниже сведения навигации в моделях hello NavHistoryData класса пользователя.</span><span class="sxs-lookup"><span data-stu-id="700f2-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="700f2-429">Он содержит основные сведения, такие как идентификатор пользователя hello, hello URL-адрес доступ и hello времени доступа.</span><span class="sxs-lookup"><span data-stu-id="700f2-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="700f2-430">Hello NavHistoryDataMonitor класс отвечает за буферизацию hello пользовательской навигации данных toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="700f2-431">Он содержит метод RecordUserNavigationEntry, который отвечает вызовом события **OnAdded** .</span><span class="sxs-lookup"><span data-stu-id="700f2-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="700f2-432">Hello следующем коде показана логика hello конструктора, использующего Rx toocreate наблюдаемой коллекции на основе события hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="700f2-433">Затем он подписывается toothis наблюдаемую коллекцию с помощью метода hello буфера.</span><span class="sxs-lookup"><span data-stu-id="700f2-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="700f2-434">перегрузка Hello указывает этого буфера hello должны отправляться каждые 20 секунд или 1000 элементов.</span><span class="sxs-lookup"><span data-stu-id="700f2-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="700f2-435">Hello обработчик преобразует все элементы в буфер hello в тип возвращающих табличные значения, а затем передает этой tooa хранимой процедуры тип пакета hello процессов.</span><span class="sxs-lookup"><span data-stu-id="700f2-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="700f2-436">Hello следующем примере кода показано полное определение hello NavHistoryDataEventArgs и классы NavHistoryDataMonitor hello hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="700f2-437">toouse этого класса буферизации приложение hello создает статический объект NavHistoryDataMonitor.</span><span class="sxs-lookup"><span data-stu-id="700f2-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="700f2-438">Каждый раз, пользователь обращается к странице, приложение hello вызывает метод NavHistoryDataMonitor.RecordUserNavigationEntry hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="700f2-439">Логика буферизации Hello продолжается tootake заботиться о отправки следующих записей toohello баз данных в пакетах.</span><span class="sxs-lookup"><span data-stu-id="700f2-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="700f2-440">Основная и подробная информация</span><span class="sxs-lookup"><span data-stu-id="700f2-440">Master detail</span></span>
<span data-ttu-id="700f2-441">Параметры, которые возвращают табличное значение, используются в простых сценариях с использованием инструкции INSERT.</span><span class="sxs-lookup"><span data-stu-id="700f2-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="700f2-442">Тем не менее он может быть более сложной toobatch вставок, работающих с более одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="700f2-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="700f2-443">Хорошим примером является сценарий Hello «основной/подробности».</span><span class="sxs-lookup"><span data-stu-id="700f2-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="700f2-444">Hello главная таблица определяет hello основной сущности.</span><span class="sxs-lookup"><span data-stu-id="700f2-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="700f2-445">Одна или несколько таблиц, детализации хранить больше данных о сущности hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="700f2-446">В этом случае связи по внешнему ключу обеспечивают связь hello сведения tooa уникальной основной сущностью.</span><span class="sxs-lookup"><span data-stu-id="700f2-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="700f2-447">Рассмотрим упрощенную версию таблицы PurchaseOrder и связанной с ней таблицы OrderDetail.</span><span class="sxs-lookup"><span data-stu-id="700f2-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="700f2-448">Привет, следуя Transact-SQL создает таблицу PurchaseOrder hello с четырьмя столбцами: OrderID, OrderDate, CustomerID и состояние.</span><span class="sxs-lookup"><span data-stu-id="700f2-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="700f2-449">Каждый заказ содержит информацию об одной или нескольких покупках товара.</span><span class="sxs-lookup"><span data-stu-id="700f2-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="700f2-450">Эти сведения сохраняются в таблице PurchaseOrderDetail hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="700f2-451">Привет, следуя Transact-SQL создает таблицу hello PurchaseOrderDetail с пятью столбцами: OrderID, OrderDetailID, ProductID, UnitPrice и OrderQty.</span><span class="sxs-lookup"><span data-stu-id="700f2-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="700f2-452">столбец OrderID Hello таблицы PurchaseOrderDetail hello должен ссылаться на заказ из таблицы PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="700f2-453">После определения внешнего ключа Hello принудительно вводит это ограничение.</span><span class="sxs-lookup"><span data-stu-id="700f2-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="700f2-454">В порядке toouse табличное значение параметров необходимо иметь один определяемый пользователем табличный тип для каждой целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="700f2-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="700f2-455">Затем определите хранимую процедуру, которая принимает таблицы этих типов.</span><span class="sxs-lookup"><span data-stu-id="700f2-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="700f2-456">Эта процедура позволяет пакет приложения toolocally набор заказов и сведения о заказе в рамках одного вызова.</span><span class="sxs-lookup"><span data-stu-id="700f2-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="700f2-457">Hello следующий запрос Transact-SQL предоставляет hello полное объявление хранимой процедуры для этого примера заказа на покупку.</span><span class="sxs-lookup"><span data-stu-id="700f2-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="700f2-458">В этом примере hello локально определенные @IdentityLink таблице хранятся hello фактические значения OrderID из hello вновь вставке строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="700f2-459">Эти идентификаторы заказов отличаются от временных значений OrderID hello в hello @orders и @details табличное значение параметров.</span><span class="sxs-lookup"><span data-stu-id="700f2-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="700f2-460">По этой причине hello @IdentityLink таблицы подключает hello OrderID значения из hello @orders параметр toohello реальные OrderID значения для hello новых строк в таблице PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="700f2-461">После выполнения этого шага hello @IdentityLink таблицы может упростить вставку подробностей заказа hello с hello фактическое OrderID, удовлетворяющий hello ограничение внешнего ключа.</span><span class="sxs-lookup"><span data-stu-id="700f2-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="700f2-462">Эту хранимую процедуру можно использовать из кода или из других вызовов Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="700f2-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="700f2-463">В разделе hello табличное значение параметров в этом документе для примера кода.</span><span class="sxs-lookup"><span data-stu-id="700f2-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="700f2-464">Привет, следуя Transact-SQL показывает, как toocall hello sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="700f2-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="700f2-465">Это решение позволяет toouse каждого пакета набор значений OrderID, которые начинаются с 1.</span><span class="sxs-lookup"><span data-stu-id="700f2-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="700f2-466">Эти временные значения OrderID описывают связи hello в пакете hello, но фактические значения OrderID hello определяются во время операции вставки hello hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="700f2-467">Можно выполнениях hello и те же операторы в предыдущем примере hello и сформировать уникальные заказы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="700f2-468">Поэтому рассмотрите возможность добавления дополнительного кода или логики базы данных, которые не допустят повторения заказов при использовании этого метода пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="700f2-469">В этом примере показано, что с помощью параметров, которые возвращают табличное значение, в пакет можно включить даже такие сложные операции с базой данных, как операции с основной и подробной информацией.</span><span class="sxs-lookup"><span data-stu-id="700f2-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="700f2-470">Операция UPSERT</span><span class="sxs-lookup"><span data-stu-id="700f2-470">UPSERT</span></span>
<span data-ttu-id="700f2-471">Другой случай использования пакетной обработки подразумевает одновременное обновление существующих и вставку новых строк.</span><span class="sxs-lookup"><span data-stu-id="700f2-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="700f2-472">Эта операция иногда является ссылка tooas операции «Вставки-обновления» (update + insert).</span><span class="sxs-lookup"><span data-stu-id="700f2-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="700f2-473">Вместо выполнения отдельных вызовов tooINSERT и UPDATE, инструкция MERGE hello осуществляется лучше всего подходит toothis.</span><span class="sxs-lookup"><span data-stu-id="700f2-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="700f2-474">Hello инструкцию MERGE можно выполнять вставки и обновления в рамках одного вызова.</span><span class="sxs-lookup"><span data-stu-id="700f2-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="700f2-475">Возвращающие табличные значения параметры могут использоваться с hello MERGE инструкции tooperform обновления и вставки.</span><span class="sxs-lookup"><span data-stu-id="700f2-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="700f2-476">Например, рассмотрим таблицу Employee упрощенный, содержит следующие столбцы hello: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="700f2-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="700f2-477">В этом примере можно использовать hello фактов, hello SocialSecurityNumber является уникальным tooperform СЛИЯНИЯ нескольких сотрудников.</span><span class="sxs-lookup"><span data-stu-id="700f2-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="700f2-478">Сначала создайте hello определяемого пользователем табличного типа.</span><span class="sxs-lookup"><span data-stu-id="700f2-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="700f2-479">Далее создайте хранимую процедуру или написать код, которая использует hello tooperform hello MERGE инструкции update и insert.</span><span class="sxs-lookup"><span data-stu-id="700f2-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="700f2-480">Hello следующий пример использует инструкцию MERGE hello для возвращающих табличные значения параметра, @employees, EmployeeTableType типа.</span><span class="sxs-lookup"><span data-stu-id="700f2-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="700f2-481">Здравствуйте, содержимое hello @employees таблицы здесь не показаны.</span><span class="sxs-lookup"><span data-stu-id="700f2-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="700f2-482">Дополнительные сведения см. в разделе документации hello и примеры для инструкции MERGE hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="700f2-483">Несмотря на то, что приветствия же работа может быть выполнена в несколько шагов вызова хранимой процедуры с помощью отдельных операций INSERT и UPDATE, hello инструкции MERGE является более эффективным.</span><span class="sxs-lookup"><span data-stu-id="700f2-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="700f2-484">Код базы данных можно также создать вызовы Transact-SQL, использующих hello инструкции MERGE напрямую без необходимости двух вызовов базы данных для INSERT и UPDATE.</span><span class="sxs-lookup"><span data-stu-id="700f2-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="700f2-485">Сводка рекомендаций</span><span class="sxs-lookup"><span data-stu-id="700f2-485">Recommendation summary</span></span>
<span data-ttu-id="700f2-486">Hello ниже приведены Сводка hello пакетной обработки рекомендации, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="700f2-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="700f2-487">Используйте буферизацию и пакетную обработку tooincrease hello производительность и масштабируемость приложений баз данных SQL.</span><span class="sxs-lookup"><span data-stu-id="700f2-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="700f2-488">Понимать hello компромисса между пакетной обработкой или буферизацией и устойчивостью приложения.</span><span class="sxs-lookup"><span data-stu-id="700f2-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="700f2-489">Во время сбоя роли hello риск потери необработанного пакета важных бизнес-данных может перевесить выигрыш производительности hello пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="700f2-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="700f2-490">Попробуйте tookeep все вызовы toohello базы данных с задержкой tooreduce одного центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="700f2-491">Если выбран метод с отправкой одного возвращающих табличные значения параметры обеспечивают hello наилучшую производительность и гибкость.</span><span class="sxs-lookup"><span data-stu-id="700f2-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="700f2-492">Для hello быстрым добавлять производительности, общие рекомендации при этом протестируйте свой сценарий:</span><span class="sxs-lookup"><span data-stu-id="700f2-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="700f2-493">Для < 100 строк используйте одну параметризованную команду INSERT.</span><span class="sxs-lookup"><span data-stu-id="700f2-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="700f2-494">Для < 1000 строк используйте параметры, которые возвращают табличное значение.</span><span class="sxs-lookup"><span data-stu-id="700f2-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="700f2-495">Для >= 1000 строк используйте SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="700f2-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="700f2-496">Для обновления и операции удаления, используйте табличное значение параметров с помощью хранимой процедуры логику, определяющую hello правильную операцию для каждой строки в параметр таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="700f2-497">Рекомендации по размеру пакета.</span><span class="sxs-lookup"><span data-stu-id="700f2-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="700f2-498">Используйте hello большие размеры пакетов, подходящие для вашего приложения и бизнес-требований.</span><span class="sxs-lookup"><span data-stu-id="700f2-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="700f2-499">Прирост производительности hello баланс больших пакетов с hello риск использования временных или неожиданных отказов.</span><span class="sxs-lookup"><span data-stu-id="700f2-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="700f2-500">Что такое hello последствия повторного выполнения операций или потери данных hello в пакете hello</span><span class="sxs-lookup"><span data-stu-id="700f2-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="700f2-501">Протестируйте tooverify пакета размер hello для наибольшего, база данных SQL не отклоняет его.</span><span class="sxs-lookup"><span data-stu-id="700f2-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="700f2-502">Создание параметров конфигурации, управляющие пакетной обработкой, такие как размер пакета hello или буферизации временное окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="700f2-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="700f2-503">Эти параметры дают возможность гибко управлять пакетной обработкой.</span><span class="sxs-lookup"><span data-stu-id="700f2-503">These settings provide flexibility.</span></span> <span data-ttu-id="700f2-504">Можно изменить поведение в рабочей среде объединения без повторного развертывания облачной службы hello hello.</span><span class="sxs-lookup"><span data-stu-id="700f2-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="700f2-505">Избегайте параллельного выполнения пакетов, которые используют одну таблицу в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="700f2-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="700f2-506">Если вы решите toodivide один пакет на несколько рабочих потоков, выполните тесты toodetermine hello оптимальное количество потоков.</span><span class="sxs-lookup"><span data-stu-id="700f2-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="700f2-507">После достижения неопределенного порогового значения большее число потоков уменьшит производительность, а не повысит ее.</span><span class="sxs-lookup"><span data-stu-id="700f2-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="700f2-508">Рассмотрите буферизацию операций по количеству и времени в качестве способа реализации пакетной обработки для нескольких сценариев.</span><span class="sxs-lookup"><span data-stu-id="700f2-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="700f2-509">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="700f2-509">Next steps</span></span>
<span data-ttu-id="700f2-510">В этой статье основное внимание уделено как структура базы данных и методы написания кода, связанные toobatching может повысить производительность приложения и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="700f2-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="700f2-511">Но это всего лишь один фактор в общей стратегии.</span><span class="sxs-lookup"><span data-stu-id="700f2-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="700f2-512">Дополнительные способы tooimprove производительности и масштабируемости в разделе [руководство по производительности базы данных SQL Azure для отдельных баз данных](sql-database-performance-guidance.md) и [вопросы цены и производительности для эластичного пула](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="700f2-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

