---
title: "технологии SQL базы данных в памяти aaaAzure | Документы Microsoft"
description: "Технологии Azure SQL базы данных в памяти значительно повысить производительность hello транзакций и аналитических рабочих нагрузок. Узнайте, как tootake преимущества этих технологий."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="7f63e-104">Оптимизация производительности с помощью технологий обработки в оперативной памяти в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="7f63e-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="7f63e-105">С помощью технологий обработки в оперативной памяти, доступных в базе данных SQL Azure, можно добиться улучшения производительности при различных рабочих нагрузках: транзакции (интерактивная обработка транзакций (OLTP)), аналитические операции (интерактивная аналитическая обработка (OLAP)) и нагрузки смешанного типа (гибридная транзакционная и аналитическая обработка (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="7f63e-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="7f63e-106">Из-за Здравствуйте эффективность запросов и обработки транзакций, технологии в памяти также помогают tooreduce затрат.</span><span class="sxs-lookup"><span data-stu-id="7f63e-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="7f63e-107">Обычно не требуется tooupgrade hello ценовой категории для повышения производительности tooachieve hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="7f63e-108">В некоторых случаях можно даже будет уменьшить hello ценовой категории, во время по-прежнему присутствует повышена производительность и технологии в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="7f63e-109">Ниже приведены два примера как помогла toosignificantly повысить производительность в OLTP в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="7f63e-110">С помощью In-Memory OLTP [кворума бизнес-решений было своей рабочей нагрузки может toodouble при одновременном повышении Dtu на 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="7f63e-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="7f63e-111">DTU обозначает *единицы передачи данных*. Этот параметр содержит оценку потребления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7f63e-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="7f63e-112">Hello следующее видео демонстрирует значительное улучшение в потреблении ресурсов с пример рабочей нагрузки: [In-Memory OLTP в базе данных SQL Azure видео](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="7f63e-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="7f63e-113">Дополнительные сведения см. в разделе hello записи блога: [In-Memory OLTP в записи блога Azure SQL базы данных](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="7f63e-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="7f63e-114">Технологии в памяти доступны во всех базах данных уровня Premium hello, включая базы данных в пулах эластичных Premium.</span><span class="sxs-lookup"><span data-stu-id="7f63e-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="7f63e-115">Hello следующие видео объясняет выигрыш производительности с технологиями в памяти в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7f63e-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="7f63e-116">Помните, что hello прироста производительности, которое вы видите всегда зависит от многих факторов, включая hello характер рабочей нагрузки hello и данных, шаблон доступа hello базы данных и т. д.</span><span class="sxs-lookup"><span data-stu-id="7f63e-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="7f63e-117">База данных SQL Azure состоит из следующих технологий памяти hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="7f63e-118">*In-Memory OLTP* повышает пропускную способность и сокращает задержки при обработке транзакций.</span><span class="sxs-lookup"><span data-stu-id="7f63e-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="7f63e-119">Выполняющуюся в памяти OLTP полезно использовать в следующих сценариях: обработка транзакций с высокой пропускной способностью, например для торговли и игр, прием данных о событиях или устройствах Интернета вещей, кэширование, загрузка данных, использование временных таблиц и табличных переменных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="7f63e-120">*Кластеризованные индексы columnstore* уменьшить объем хранилища (времен too10) и повысить производительность запросов, отчетов и аналитики.</span><span class="sxs-lookup"><span data-stu-id="7f63e-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="7f63e-121">Можно использовать с таблицами фактов в вашей toofit витринах данных больше данных в базе данных и повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="7f63e-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="7f63e-122">Кроме того можно использовать со статистическими данными в вашей рабочей базы данных tooarchive и быть может tooquery too10 времени больше данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="7f63e-123">*Некластеризованные индексы columnstore* HTAP справку в режиме реального времени анализировать toogain ваш бизнес через запрос hello рабочей базы данных напрямую, без необходимости toorun hello дорогих извлечения, преобразования и процесса загрузки (ETL) и ожидания для заполнения hello toobe хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="7f63e-124">Некластеризованные индексы columnstore разрешает быстрого выполнения аналитических запросов на базы данных OLTP hello, одновременно уменьшая hello влияние на hello рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7f63e-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="7f63e-125">Также возможно сочетание hello оптимизированных для памяти таблицы с индексом columnstore.</span><span class="sxs-lookup"><span data-stu-id="7f63e-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="7f63e-126">Это сочетание позволяет очень быстро транзакции tooperform обработки и слишком*одновременно* выполнения analytics запрашивает очень быстро на hello же данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="7f63e-127">Индексы columnstore и In-Memory OLTP были частью hello продукта SQL Server 2012 и 2014, соответственно.</span><span class="sxs-lookup"><span data-stu-id="7f63e-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="7f63e-128">Azure базы данных SQL и SQL Server используют hello же реализации технологии в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="7f63e-129">При этом новые возможности сначала предоставляются для базы данных SQL Azure, а затем выпускаются для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7f63e-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="7f63e-130">В этом разделе описываются аспекты In-Memory OLTP и columnstore индексы, определенные tooAzure базы данных SQL и содержит также фрагменты кода:</span><span class="sxs-lookup"><span data-stu-id="7f63e-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="7f63e-131">Вы увидите hello влияние этих технологий на хранение данных и ограничения на размер.</span><span class="sxs-lookup"><span data-stu-id="7f63e-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="7f63e-132">Вы увидите, как toomanage hello перемещения баз данных, которые используют эти технологии между hello различным ценовым категориям.</span><span class="sxs-lookup"><span data-stu-id="7f63e-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="7f63e-133">Вы увидите два примеры, иллюстрирующие использование hello In-Memory OLTP, а также индексов columnstore в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7f63e-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="7f63e-134">См. следующие ресурсы для получения дополнительной информации hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-134">See hello following resources for more information.</span></span>

<span data-ttu-id="7f63e-135">Подробные сведения о технологиях hello:</span><span class="sxs-lookup"><span data-stu-id="7f63e-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="7f63e-136">[Общие сведения о OLTP в памяти и сценариях использования](https://msdn.microsoft.com/library/mt774593.aspx) (включает примеры использования toocustomer ссылки и сведения tooget работы)</span><span class="sxs-lookup"><span data-stu-id="7f63e-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="7f63e-137">In-Memory OLTP (оптимизация в памяти)</span><span class="sxs-lookup"><span data-stu-id="7f63e-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="7f63e-138">Описание индексов columnstore</span><span class="sxs-lookup"><span data-stu-id="7f63e-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="7f63e-139">Гибридные сценарии транзакционной и аналитической обработки, которые также называются [операционной аналитикой в реальном времени](https://msdn.microsoft.com/library/dn817827.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f63e-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="7f63e-140">Краткое руководство по In-Memory OLTP: [краткое руководство 1: технологии выполнения OLTP в памяти для быстрее производительности T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (Начало работы другого toohelp статье)</span><span class="sxs-lookup"><span data-stu-id="7f63e-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="7f63e-141">Подробные видеоролики о технологиях hello:</span><span class="sxs-lookup"><span data-stu-id="7f63e-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="7f63e-142">[In-Memory OLTP в базе данных SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (который содержит демонстрационную версию производительности преимущества и шаги tooreproduce эти результаты самостоятельно)</span><span class="sxs-lookup"><span data-stu-id="7f63e-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="7f63e-143">In-Memory OLTP видео: Что это такое и когда/как toouse его</span><span class="sxs-lookup"><span data-stu-id="7f63e-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- <span data-ttu-id="7f63e-144">[Columnstore Index: In-Memory Analytics (i.e. columnstore index) Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/) (Видео о выполняющейся в памяти аналитике (например, индексах columnstore) с конференции Ignite 2016).</span><span class="sxs-lookup"><span data-stu-id="7f63e-144">[Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)</span></span>

## <a name="storage-and-data-size"></a><span data-ttu-id="7f63e-145">Емкость хранилища и объем данных</span><span class="sxs-lookup"><span data-stu-id="7f63e-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="7f63e-146">Ограничения на объем данных и емкость хранилища для In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="7f63e-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="7f63e-147">In-Memory OLTP включает оптимизированные для памяти таблицы, которые используются для хранения пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="7f63e-148">Эти таблицы являются обязательным toofit в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="7f63e-149">Так как вы управляете памяти непосредственно в hello служба базы данных SQL, у нас есть концепция hello квоты для пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="7f63e-150">Идея является ссылка tooas *хранилища In-Memory OLTP*.</span><span class="sxs-lookup"><span data-stu-id="7f63e-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="7f63e-151">Каждая поддерживаемая ценовая категория отдельных баз данных и пулов эластичных баз данных включает некоторый объем хранилища выполняющейся в памяти OLTP.</span><span class="sxs-lookup"><span data-stu-id="7f63e-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="7f63e-152">На момент написания статьи hello вы получаете один гигабайт хранилища для каждого 125 единицы транзакций баз данных (Dtu) или эластичной базы данных единицы транзакций (Edtu).</span><span class="sxs-lookup"><span data-stu-id="7f63e-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="7f63e-153">Hello [уровней обслуживания базы данных SQL](sql-database-service-tiers.md) статья имеет hello официальный список hello In-Memory OLTP доступного хранилища для каждого поддерживаемого Автономная база данных и ценовой категории эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="7f63e-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="7f63e-154">Привет, следующие элементы, учитываются украшение хранилища In-Memory OLTP:</span><span class="sxs-lookup"><span data-stu-id="7f63e-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="7f63e-155">Активные строки пользовательских данных в оптимизированных для памяти таблицах и переменных таблиц.</span><span class="sxs-lookup"><span data-stu-id="7f63e-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="7f63e-156">Обратите внимание, что старых версий строк не учитываются при определении hello cap.</span><span class="sxs-lookup"><span data-stu-id="7f63e-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="7f63e-157">Индексы оптимизированных для памяти таблиц.</span><span class="sxs-lookup"><span data-stu-id="7f63e-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="7f63e-158">Операционные затраты на операции ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="7f63e-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="7f63e-159">При достижении конца hello появляется сообщение об ошибке out из квоты и вы больше не будет tooinsert или обновления данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="7f63e-160">toomitigate эту ошибку, удалите данные или увеличьте hello ценовой категории базы данных hello или пула.</span><span class="sxs-lookup"><span data-stu-id="7f63e-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="7f63e-161">Дополнительные сведения о мониторинге использования хранилища In-Memory OLTP и настройка оповещений по достижении конца hello почти см. в разделе [монитор в памяти хранилища](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="7f63e-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="7f63e-162">О пулах эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="7f63e-162">About elastic pools</span></span>

<span data-ttu-id="7f63e-163">При использовании пулов эластичных hello хранилища In-Memory OLTP совместно среди всех баз данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="7f63e-164">Таким образом использование hello в одной базе данных может влиять на другие базы данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="7f63e-165">Есть два пути устранения таких проблем.</span><span class="sxs-lookup"><span data-stu-id="7f63e-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="7f63e-166">Настройте Max-eDTU для баз данных, меньше, чем число hello eDTU пула hello в целом.</span><span class="sxs-lookup"><span data-stu-id="7f63e-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="7f63e-167">Использование хранилища In-Memory OLTP hello в любой базе данных в пуле hello, размер toohello, соответствующее число eDTU toohello для креплений максимального.</span><span class="sxs-lookup"><span data-stu-id="7f63e-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="7f63e-168">Установите для баз данных параметр Min-eDTU больше нуля.</span><span class="sxs-lookup"><span data-stu-id="7f63e-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="7f63e-169">Это минимальный гарантирует, что каждая база данных в пуле hello имеет hello объем доступного хранилища In-Memory OLTP, соответствующий toohello настроен Min eDTU.</span><span class="sxs-lookup"><span data-stu-id="7f63e-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="7f63e-170">Размер данных и хранилище для индексов сolumnstore</span><span class="sxs-lookup"><span data-stu-id="7f63e-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="7f63e-171">Индексы ColumnStore не требуется toofit в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="7f63e-172">Таким образом, hello только ограничение на размер hello hello индексов является hello максимальный общий размер базы данных, который описан в hello [уровней обслуживания базы данных SQL](sql-database-service-tiers.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="7f63e-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="7f63e-173">При использовании кластеризованных индексов, столбцам сжатия используется для хранения базовой таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="7f63e-174">Такое сжатие может значительно уменьшить объем хранилища hello данные пользователей, это означает, что может поместиться больше данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="7f63e-175">И hello сжатия может быть увеличено с [столбцам архивного сжатия](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="7f63e-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="7f63e-176">Hello степень сжатия, можно добиться зависит от природы hello hello данных, но 10 раз hello сжатия не возникают.</span><span class="sxs-lookup"><span data-stu-id="7f63e-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="7f63e-177">Например если имеется база данных размером до 1 терабайт (ТБ) и добиться сжатия hello 10 раз с помощью индексов columnstore, может удовлетворить всего 10 ТБ пользовательских данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="7f63e-178">При использовании некластеризованных индексов columnstore hello базовой таблицы все еще хранятся в формате традиционных rowstore hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="7f63e-179">Таким образом hello экономии пространства хранения, не являются большим, чем с кластеризованными индексами columnstore.</span><span class="sxs-lookup"><span data-stu-id="7f63e-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="7f63e-180">Тем не менее при замене число традиционной некластеризованные индексы с одним индексом columnstore, по-прежнему видно общей экономии hello сократить объем хранилища для таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="7f63e-181">Изменение ценовых категорий баз данных, использующих технологии обработки в оперативной памяти</span><span class="sxs-lookup"><span data-stu-id="7f63e-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="7f63e-182">Не может находиться любые проблемы совместимости или других проблем при обновлении tooa ценовой категории, такие как из стандартных tooPremium более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7f63e-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="7f63e-183">доступные функции Hello и ресурсы только повысить.</span><span class="sxs-lookup"><span data-stu-id="7f63e-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="7f63e-184">Но переходе hello ценовой категории может отрицательно повлиять на базу данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="7f63e-185">влияние Hello особенно очевиден при переходе с Premium tooStandard или Basic, когда база данных содержит объекты OLTP в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="7f63e-186">Оптимизированные для памяти таблицы и индексы columnstore будут недоступны после понижения hello (даже если они оставались видимыми).</span><span class="sxs-lookup"><span data-stu-id="7f63e-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="7f63e-187">Hello же рекомендации применяются, когда понижение hello ценовой категории пула эластичных БД или перемещение базы данных при использовании технологии в памяти, в стандартный или базовой эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="7f63e-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="7f63e-188">In-Memory OLTP;</span><span class="sxs-lookup"><span data-stu-id="7f63e-188">In-Memory OLTP</span></span>

<span data-ttu-id="7f63e-189">*Понижение уровня tooBasic/Standard*: OLTP в памяти не поддерживается в базах данных уровня Standard и Basic hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="7f63e-190">Кроме того это не значит возможных toomove базу данных с любой toohello объектов In-Memory OLTP уровня Standard и Basic.</span><span class="sxs-lookup"><span data-stu-id="7f63e-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="7f63e-191">До возврата к предыдущей версии базы данных hello tooStandard и простой, удалите все таблицы, оптимизированные для памяти табличных типов, а также всех скомпилированных в собственном коде модулей T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7f63e-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="7f63e-192">Нет toounderstand программный способ поддержку данной базы данных OLTP в памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="7f63e-193">Можно выполнить приветствия при следующем запросе Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="7f63e-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="7f63e-194">Если запрос hello возвращает **1**, In-Memory OLTP поддерживается в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="7f63e-195">*Понижение уровня tooa нижнего уровня Premium*: данные в таблицах, оптимизированных для памяти должны умещаться в хранилища In-Memory OLTP hello, связан с ценовой категории базы данных hello hello, или в hello эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="7f63e-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="7f63e-196">При попытке hello toolower ценовой категории или перемещение базы данных hello в пул, не имеет достаточно свободного In-Memory OLTP, hello операция заканчивается неудачно.</span><span class="sxs-lookup"><span data-stu-id="7f63e-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="7f63e-197">Индексы columnstore</span><span class="sxs-lookup"><span data-stu-id="7f63e-197">Columnstore indexes</span></span>

<span data-ttu-id="7f63e-198">*Понижение уровня tooBasic или Standard*: Columnstore, индексы поддерживаются только в ценовой категории "премиум" hello, а не в hello уровней Standard и Basic.</span><span class="sxs-lookup"><span data-stu-id="7f63e-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="7f63e-199">При переходе с tooStandard базы данных или Basic, индекс columnstore становится недоступной.</span><span class="sxs-lookup"><span data-stu-id="7f63e-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="7f63e-200">Hello система сохраняет индекс columnstore, но он никогда не использует индекс hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="7f63e-201">При обновлении позже tooPremium назад, индекс columnstore является немедленно готовы toobe попытку использовать.</span><span class="sxs-lookup"><span data-stu-id="7f63e-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="7f63e-202">Если у вас есть **кластеризованный** индекс columnstore hello вся таблица становится недоступным после понижения уровня.</span><span class="sxs-lookup"><span data-stu-id="7f63e-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="7f63e-203">Корпорация Майкрософт рекомендует удалить все *кластеризованный* перед переходе базы данных ниже уровня Premium hello индексов columnstore.</span><span class="sxs-lookup"><span data-stu-id="7f63e-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="7f63e-204">*Понижение уровня tooa нижнего уровня Premium*: этот переход к более раннему завершается успешно, если hello вся база данных помещается в hello максимальный размер базы данных для целевого объекта hello ценовой категории, или внутри hello доступного хранилища в пуле эластичных БД hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="7f63e-205">Отсутствует влияние конкретных hello индексов columnstore.</span><span class="sxs-lookup"><span data-stu-id="7f63e-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="7f63e-206">1. Установите образец hello In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="7f63e-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="7f63e-207">Можно создать с помощью нескольких щелчков в hello учебной базой данных AdventureWorksLT hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7f63e-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7f63e-208">Затем hello действия, описанные в этом разделе объясняется, как можно дополнить базе данных AdventureWorksLT с объектами OLTP в памяти и продемонстрировать преимущества производительности.</span><span class="sxs-lookup"><span data-stu-id="7f63e-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="7f63e-209">Упрощенная, но одновременно более наглядная демонстрация выполняющейся в памяти OLTP представлена здесь:</span><span class="sxs-lookup"><span data-stu-id="7f63e-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="7f63e-210">Выпуск: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="7f63e-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="7f63e-211">Исходный код: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="7f63e-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="7f63e-212">Шаги установки</span><span class="sxs-lookup"><span data-stu-id="7f63e-212">Installation steps</span></span>

1. <span data-ttu-id="7f63e-213">В hello [портал Azure](https://portal.azure.com/), создание расширенной базы данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="7f63e-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="7f63e-214">Набор hello **источника** toohello учебной базой данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="7f63e-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="7f63e-215">Подробные инструкции см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f63e-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="7f63e-216">Подключение базы данных toohello с SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f63e-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="7f63e-217">Копировать hello [сценарий In-Memory OLTP Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="7f63e-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="7f63e-218">Hello скрипт T-SQL создает необходимые в памяти объекты hello в hello AdventureWorksLT образца базы данных, созданной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="7f63e-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="7f63e-219">Вставьте скрипт T-SQL hello в SSMS и затем выполнить сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="7f63e-220">Hello `MEMORY_OPTIMIZED = ON` предложение инструкции CREATE TABLE имеют большое значение.</span><span class="sxs-lookup"><span data-stu-id="7f63e-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="7f63e-221">Например:</span><span class="sxs-lookup"><span data-stu-id="7f63e-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="7f63e-222">Ошибка 40536</span><span class="sxs-lookup"><span data-stu-id="7f63e-222">Error 40536</span></span>


<span data-ttu-id="7f63e-223">Если появляется ошибка 40536 при запуске скрипта hello T-SQL, выполните следующие tooverify скрипт T-SQL, hello поддерживает ли база данных в памяти hello:</span><span class="sxs-lookup"><span data-stu-id="7f63e-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="7f63e-224">Значение **0** указывает на то, что обработка в оперативной памяти не поддерживается, а значение **1** — наоборот.</span><span class="sxs-lookup"><span data-stu-id="7f63e-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="7f63e-225">проблема toodiagnose hello, гарантировать hello базы данных уровня Premium hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="7f63e-226">О hello созданных элементов, оптимизированных для памяти</span><span class="sxs-lookup"><span data-stu-id="7f63e-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="7f63e-227">**Таблицы**: пример hello содержит hello в следующей таблице, оптимизированной для памяти:</span><span class="sxs-lookup"><span data-stu-id="7f63e-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="7f63e-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="7f63e-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="7f63e-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="7f63e-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="7f63e-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="7f63e-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="7f63e-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="7f63e-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="7f63e-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="7f63e-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="7f63e-233">Вы можете проверить оптимизированных для памяти таблиц с помощью hello **обозревателя объектов** в среде SSMS.</span><span class="sxs-lookup"><span data-stu-id="7f63e-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="7f63e-234">Щелкните правой кнопкой мыши **Таблицы** > **Фильтры** > **Параметры фильтров** > **Оптимизирован для памяти**.</span><span class="sxs-lookup"><span data-stu-id="7f63e-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="7f63e-235">Hello значение равно 1.</span><span class="sxs-lookup"><span data-stu-id="7f63e-235">hello value equals 1.</span></span>


<span data-ttu-id="7f63e-236">Или можно также запросить представления каталога hello, такие как:</span><span class="sxs-lookup"><span data-stu-id="7f63e-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="7f63e-237">**Скомпилированная в собственном коде хранимая процедура**: процедуру SalesLT.usp_InsertSalesOrder_inmem можно проверить с помощью запроса представления каталога.</span><span class="sxs-lookup"><span data-stu-id="7f63e-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="7f63e-238">Запустите рабочую нагрузку OLTP образец hello</span><span class="sxs-lookup"><span data-stu-id="7f63e-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="7f63e-239">Здравствуйте разность двух следующих hello *хранимых процедур* hello первая процедура использует оптимизированных для памяти версии таблиц hello, при hello вторая процедура использует hello обычных таблицах на диске:</span><span class="sxs-lookup"><span data-stu-id="7f63e-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="7f63e-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="7f63e-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="7f63e-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="7f63e-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="7f63e-242">В этом разделе, показано, как toouse hello под рукой **ostress.exe** tooexecute программа hello две хранимые процедуры на стрессовые уровнях.</span><span class="sxs-lookup"><span data-stu-id="7f63e-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="7f63e-243">Можно сравнить, сколько времени занимает toofinish запусков нагрузочных hello двух.</span><span class="sxs-lookup"><span data-stu-id="7f63e-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="7f63e-244">При запуске ostress.exe, мы рекомендуем передавать значения параметров, предназначенных для обоих следующих hello:</span><span class="sxs-lookup"><span data-stu-id="7f63e-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="7f63e-245">-n100 — для выполнения большого количества одновременных подключений;</span><span class="sxs-lookup"><span data-stu-id="7f63e-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="7f63e-246">-r500 — для многократного (сотни раз) выполнения каждого цикла подключения.</span><span class="sxs-lookup"><span data-stu-id="7f63e-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="7f63e-247">Тем не менее может потребоваться toostart с намного меньше значения, такие как - n10 и - r50 tooensure, что все работает.</span><span class="sxs-lookup"><span data-stu-id="7f63e-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="7f63e-248">Скрипт для ostress.exe</span><span class="sxs-lookup"><span data-stu-id="7f63e-248">Script for ostress.exe</span></span>


<span data-ttu-id="7f63e-249">В этом разделе отображается hello скрипт T-SQL, внедренный в наших ostress.exe командной строки.</span><span class="sxs-lookup"><span data-stu-id="7f63e-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="7f63e-250">Hello скрипт использует элементы, которые были созданы путем hello скрипт T-SQL, которое ранее было установлено.</span><span class="sxs-lookup"><span data-stu-id="7f63e-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="7f63e-251">Hello следующий скрипт вставляет образец заказа на продажу с пятью линейными элементами в следующих hello оптимизированных для памяти *таблиц*:</span><span class="sxs-lookup"><span data-stu-id="7f63e-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="7f63e-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="7f63e-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="7f63e-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="7f63e-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="7f63e-254">toomake hello *_ondisk* версии Здравствуйте предыдущий сценарий T-SQL для ostress.exe, и замените оба экземпляра hello *_inmem* substring с *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="7f63e-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="7f63e-255">Эти замены влияет на приветствия имен таблиц и хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="7f63e-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="7f63e-256">Установка служебных программ RML и ostress</span><span class="sxs-lookup"><span data-stu-id="7f63e-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="7f63e-257">В идеальном случае следует запланировать toorun ostress.exe на виртуальной машине Azure (ВМ).</span><span class="sxs-lookup"><span data-stu-id="7f63e-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="7f63e-258">Вы создадите [виртуальной Машины Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) в hello же Azure географическом регионе, где находится базе данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="7f63e-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="7f63e-259">Но вы также можете запустить программу ostress.exe и на переносном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7f63e-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="7f63e-260">На hello виртуальной Машины или на узле все, что выбрать, установите служебные программы hello языка разметки воспроизведения (RML).</span><span class="sxs-lookup"><span data-stu-id="7f63e-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="7f63e-261">Служебные программы Hello включают ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="7f63e-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="7f63e-262">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="7f63e-262">For more information, see:</span></span>
- <span data-ttu-id="7f63e-263">Здравствуйте, обсуждение ostress.exe в [образца базы данных для In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f63e-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="7f63e-264">Или ознакомьтесь со статьей [Пример базы данных для выполняющейся в памяти OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f63e-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="7f63e-265">Hello [блога по установке ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f63e-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="7f63e-266">Запустите hello *_inmem* сначала загрузить рабочей нагрузки</span><span class="sxs-lookup"><span data-stu-id="7f63e-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="7f63e-267">Можно использовать *RML Cmd Prompt* окна toorun наших ostress.exe командной строки.</span><span class="sxs-lookup"><span data-stu-id="7f63e-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="7f63e-268">параметры командной строки Hello прямой ostress для:</span><span class="sxs-lookup"><span data-stu-id="7f63e-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="7f63e-269">параллельно выполнять 100 подключений (-n100);</span><span class="sxs-lookup"><span data-stu-id="7f63e-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="7f63e-270">У каждого соединения, запустите скрипт T-SQL hello 50 раз (-r50).</span><span class="sxs-lookup"><span data-stu-id="7f63e-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="7f63e-271">toorun hello предшествующий ostress.exe командной строки:</span><span class="sxs-lookup"><span data-stu-id="7f63e-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="7f63e-272">Сброс данных содержимое hello базы данных, выполнив следующую команду в SSMS, toodelete hello все hello данные, которые вносились во все предыдущие запуски:</span><span class="sxs-lookup"><span data-stu-id="7f63e-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="7f63e-273">Скопируйте текст hello hello предшествующий буфера tooyour ostress.exe командной строки.</span><span class="sxs-lookup"><span data-stu-id="7f63e-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="7f63e-274">Замените hello `<placeholders>` hello параметры -S - U -P -d с hello правильная реальные значения.</span><span class="sxs-lookup"><span data-stu-id="7f63e-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="7f63e-275">В окне командной строки RML запустите измененную командную строку.</span><span class="sxs-lookup"><span data-stu-id="7f63e-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="7f63e-276">Результат — это длительность выполнения теста</span><span class="sxs-lookup"><span data-stu-id="7f63e-276">Result is a duration</span></span>


<span data-ttu-id="7f63e-277">По завершении ostress.exe она записывает длительность выполнения как его последняя строка выходных данных в окне приветствия RML Cmd hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="7f63e-278">Например, более короткий тестовый запуск длится около 1,5 минут:</span><span class="sxs-lookup"><span data-stu-id="7f63e-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="7f63e-279">Сброс базы данных, изменение значения *_ondisk* и повторный запуск</span><span class="sxs-lookup"><span data-stu-id="7f63e-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="7f63e-280">После того как вы hello в результате hello *_inmem* запуска, выполните следующие шаги для hello hello *_ondisk* запуска:</span><span class="sxs-lookup"><span data-stu-id="7f63e-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="7f63e-281">Сброс hello базы данных, выполнив следующую команду в SSMS toodelete hello все данные hello добавленный hello предыдущего выполнения:</span><span class="sxs-lookup"><span data-stu-id="7f63e-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="7f63e-282">Изменить tooreplace hello ostress.exe командной строки *_inmem* с *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="7f63e-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="7f63e-283">Повторно запустите ostress.exe для hello во второй раз и записать результат длительность hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="7f63e-284">Опять же сбросьте hello базы данных (для ответственно удаление большого объема тестовых данных, которое может быть).</span><span class="sxs-lookup"><span data-stu-id="7f63e-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="7f63e-285">Ожидаемые результаты сравнения</span><span class="sxs-lookup"><span data-stu-id="7f63e-285">Expected comparison results</span></span>

<span data-ttu-id="7f63e-286">Наши тесты в памяти показали, повысить производительность **девяти раз** для этой простой рабочей нагрузки с ostress запущен на Виртуальной машине Azure в hello же регионе Azure, что hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="7f63e-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="7f63e-287">2. Установите образец hello аналитики в памяти</span><span class="sxs-lookup"><span data-stu-id="7f63e-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="7f63e-288">В этом разделе вы сравнить hello операции ввода-ВЫВОДА и статистику результатов при работе с индексом columnstore сравнению с традиционной сбалансированного дерева индекса.</span><span class="sxs-lookup"><span data-stu-id="7f63e-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="7f63e-289">Для аналитики в реальном времени рабочей нагрузки OLTP часто бывает наиболее toouse некластеризованный индекс columnstore.</span><span class="sxs-lookup"><span data-stu-id="7f63e-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="7f63e-290">Дополнительные сведения см. в статье [Руководство по индексам columnstore](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f63e-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="7f63e-291">Подготовка hello columnstore analytics теста</span><span class="sxs-lookup"><span data-stu-id="7f63e-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="7f63e-292">Используйте hello Azure портала toocreate из образца hello свежей базы данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="7f63e-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="7f63e-293">Используйте такое же имя.</span><span class="sxs-lookup"><span data-stu-id="7f63e-293">Use that exact name.</span></span>
 - <span data-ttu-id="7f63e-294">Выберите любой уровень служб категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="7f63e-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="7f63e-295">Копировать hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="7f63e-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="7f63e-296">Hello скрипт T-SQL создает необходимые в памяти объекты hello в hello AdventureWorksLT образца базы данных, созданной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="7f63e-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="7f63e-297">Hello скрипт создает таблицу измерения hello и две таблицы фактов.</span><span class="sxs-lookup"><span data-stu-id="7f63e-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="7f63e-298">таблицы фактов Hello заполняются 3.5 миллионов строк.</span><span class="sxs-lookup"><span data-stu-id="7f63e-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="7f63e-299">Hello скрипта может занять toocomplete 15 минут.</span><span class="sxs-lookup"><span data-stu-id="7f63e-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="7f63e-300">Вставьте скрипт T-SQL hello в SSMS и затем выполнить сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="7f63e-301">Hello **COLUMNSTORE** ключевое слово в hello **CREATE INDEX** большое значение, как и в инструкции:</span><span class="sxs-lookup"><span data-stu-id="7f63e-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="7f63e-302">Установите уровень toocompatibility AdventureWorksLT 130:</span><span class="sxs-lookup"><span data-stu-id="7f63e-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="7f63e-303">Уровень 130 не функции непосредственно связанная tooIn памяти.</span><span class="sxs-lookup"><span data-stu-id="7f63e-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="7f63e-304">При этом уровень 130 обычно обеспечивает более высокую скорость обработки запросов, чем уровень 120.</span><span class="sxs-lookup"><span data-stu-id="7f63e-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="7f63e-305">Ключевые таблицы и индексы columnstore</span><span class="sxs-lookup"><span data-stu-id="7f63e-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="7f63e-306">dbo. FactResellerSalesXL_CCI является таблица, которая имеет кластеризованный индекс, с расширенным сжатия на hello *данные* уровне.</span><span class="sxs-lookup"><span data-stu-id="7f63e-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="7f63e-307">dbo. FactResellerSalesXL_PageCompressed является таблица, которая имеет эквивалент регулярного кластеризованный индекс, который сжимается только на hello *страницы* уровне.</span><span class="sxs-lookup"><span data-stu-id="7f63e-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="7f63e-308">Индекс columnstore hello toocompare запросы ключей</span><span class="sxs-lookup"><span data-stu-id="7f63e-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="7f63e-309">Существуют [несколько типов запросов T-SQL, которые можно выполнить](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="7f63e-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="7f63e-310">В шаге 2 раздела hello скрипт T-SQL Обратите внимания пары toothis запросов.</span><span class="sxs-lookup"><span data-stu-id="7f63e-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="7f63e-311">Они отличаются только одной строкой.</span><span class="sxs-lookup"><span data-stu-id="7f63e-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="7f63e-312">Кластеризованный индекс находится в hello FactResellerSalesXL\_CCI таблицы.</span><span class="sxs-lookup"><span data-stu-id="7f63e-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="7f63e-313">Hello следующий фрагмент скрипта T-SQL Выводит статистику ввода-ВЫВОДА и время для запроса hello каждой таблицы.</span><span class="sxs-lookup"><span data-stu-id="7f63e-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="7f63e-314">В базе данных с hello P2 ценовую категорию можно ожидать около девяти раз hello выигрыш в производительности для этого запроса с помощью hello кластеризованный индекс, по сравнению с традиционными индексами hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="7f63e-315">P15 то можно ожидать выигрыш в производительности примерно 57 раз hello с помощью индекса columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="7f63e-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7f63e-316">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f63e-316">Next steps</span></span>

- [<span data-ttu-id="7f63e-317">Краткое руководство 1. Технологии выполнения OLTP в памяти для повышения производительности службы Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="7f63e-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="7f63e-318">Повышение производительности приложений в базе данных SQL с помощью выполняющейся в памяти OLTP</span><span class="sxs-lookup"><span data-stu-id="7f63e-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="7f63e-319">[Мониторинг хранилища OLTP в памяти](sql-database-in-memory-oltp-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="7f63e-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7f63e-320">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7f63e-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="7f63e-321">Подробные сведения</span><span class="sxs-lookup"><span data-stu-id="7f63e-321">Deeper information</span></span>

- <span data-ttu-id="7f63e-322">Узнайте, как [Quorum удваивает ключевую рабочую нагрузку на базу данных при одновременном сокращении DTU на 70 % благодаря использованию In-Memory OLTP для базы данных SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="7f63e-322">[Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>

- <span data-ttu-id="7f63e-323">[In-Memory OLTP in Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Выполняющаяся в памяти OLTP в базе данных SQL Azure)</span><span class="sxs-lookup"><span data-stu-id="7f63e-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

- <span data-ttu-id="7f63e-324">[Learn about In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx) (Знакомство с In-Memory OLTP)</span><span class="sxs-lookup"><span data-stu-id="7f63e-324">[Learn about In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx)</span></span>

- [<span data-ttu-id="7f63e-325">Руководство по индексам columnstore</span><span class="sxs-lookup"><span data-stu-id="7f63e-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="7f63e-326">Начало работы с Columnstore для получения операционной аналитики в реальном времени</span><span class="sxs-lookup"><span data-stu-id="7f63e-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="7f63e-327">Технический документ с [рекомендациями по распространенным шаблонам рабочих нагрузок и миграции](http://msdn.microsoft.com/library/dn673538.aspx) включает описание шаблонов рабочих нагрузок, для которых выполняющаяся OLTP обычно обеспечивает значительное повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="7f63e-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="7f63e-328">Проектирование приложений</span><span class="sxs-lookup"><span data-stu-id="7f63e-328">Application design</span></span>

- [<span data-ttu-id="7f63e-329">In-Memory OLTP (оптимизация в памяти)</span><span class="sxs-lookup"><span data-stu-id="7f63e-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="7f63e-330">Повышение производительности приложений в базе данных SQL с помощью выполняющейся в памяти OLTP</span><span class="sxs-lookup"><span data-stu-id="7f63e-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="7f63e-331">Средства</span><span class="sxs-lookup"><span data-stu-id="7f63e-331">Tools</span></span>

- [<span data-ttu-id="7f63e-332">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7f63e-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="7f63e-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="7f63e-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="7f63e-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="7f63e-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
