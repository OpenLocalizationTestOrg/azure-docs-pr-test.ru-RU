---
title: "Технологии обработки в оперативной памяти в базе данных SQL Azure | Документация Майкрософт"
description: "Технологии обработки в оперативной памяти в базе данных SQL Azure значительно повышают производительность транзакций и аналитических операций. Узнайте, как воспользоваться преимуществами этих технологий."
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
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="52a61-104">Оптимизация производительности с помощью технологий обработки в оперативной памяти в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="52a61-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="52a61-105">С помощью технологий обработки в оперативной памяти, доступных в базе данных SQL Azure, можно добиться улучшения производительности при различных рабочих нагрузках: транзакции (интерактивная обработка транзакций (OLTP)), аналитические операции (интерактивная аналитическая обработка (OLAP)) и нагрузки смешанного типа (гибридная транзакционная и аналитическая обработка (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="52a61-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="52a61-106">Благодаря более эффективной обработке запросов и транзакций технологии обработки в оперативной памяти также помогут снизить затраты.</span><span class="sxs-lookup"><span data-stu-id="52a61-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="52a61-107">Вам не нужно переходить на более высокую ценовую категорию баз данных, чтобы добиться повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="52a61-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="52a61-108">В некоторых случаях технологии обработки в оперативной памяти предусматривают даже переход на более низкую ценовую категорию без снижения производительности.</span><span class="sxs-lookup"><span data-stu-id="52a61-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="52a61-109">Вот несколько примеров того, как выполняющаяся в памяти OLTP помогла значительно улучшить показатели производительности:</span><span class="sxs-lookup"><span data-stu-id="52a61-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="52a61-110">Используя выполняющуюся в памяти OLTP, [компания Quorum Business Solutions смогла вдвое увеличить свои рабочие нагрузки, при этом улучшив показатели DTU на 70 %](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="52a61-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="52a61-111">DTU обозначает *единицы передачи данных*. Этот параметр содержит оценку потребления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="52a61-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="52a61-112">В следующем видеоролике на примере рабочей нагрузки показано, как достигается значительное улучшение показателей потребления ресурсов: [In-Memory OLTP in Azure SQL DB](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (Выполняющаяся в памяти OLTP в базе данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="52a61-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="52a61-113">Дополнительные сведения см. в записи блога [In-Memory OLTP in Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Выполняющаяся в памяти OLTP в базе данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="52a61-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="52a61-114">Технологии обработки в оперативной памяти доступны для всех баз данных уровня "Премиум", в том числе для пулов эластичных баз данных уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="52a61-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="52a61-115">В следующем видео демонстрируется потенциал роста производительности при использовании технологий In-Memory для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="52a61-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="52a61-116">Помните, что фактическое увеличение производительности всегда зависит от многих факторов, включая характер рабочей нагрузки и свойства данных, схему доступа к базе данных и т. д.</span><span class="sxs-lookup"><span data-stu-id="52a61-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="52a61-117">База данных SQL Azure поддерживает следующие технологии In-Memory.</span><span class="sxs-lookup"><span data-stu-id="52a61-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="52a61-118">*In-Memory OLTP* повышает пропускную способность и сокращает задержки при обработке транзакций.</span><span class="sxs-lookup"><span data-stu-id="52a61-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="52a61-119">Выполняющуюся в памяти OLTP полезно использовать в следующих сценариях: обработка транзакций с высокой пропускной способностью, например для торговли и игр, прием данных о событиях или устройствах Интернета вещей, кэширование, загрузка данных, использование временных таблиц и табличных переменных.</span><span class="sxs-lookup"><span data-stu-id="52a61-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="52a61-120">*Кластеризованные индексы columnstore* снижают требования к вместимости хранилища (иногда до 10 раз) и повышают производительность запросов для отчетов и аналитики.</span><span class="sxs-lookup"><span data-stu-id="52a61-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="52a61-121">Используйте их с таблицами фактов в киосках данных, чтобы разместить в базе больше данных и повысить ее производительность.</span><span class="sxs-lookup"><span data-stu-id="52a61-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="52a61-122">Вы также можете использовать их с данными журналов в рабочей базе данных, чтобы архивировать и запрашивать в 10 раз больше данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="52a61-123">*Некластеризованные индексы columnstore* для гибридных сценариев транзакционной и аналитической обработки помогут вам получить информацию о параметрах бизнеса в режиме реального времени, напрямую запрашивая рабочую базу данных без необходимости выполнения ресурсоемких операций извлечения, преобразования и загрузки, а также без задержек при заполнении хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="52a61-124">Некластеризованные индексы columnstore позволяют очень быстро выполнять аналитические запросы к базе данных OLTP, практически не оказывая влияния на рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="52a61-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="52a61-125">Вы также можете сочетать таблицу, оптимизированную для обработки в памяти, с индексом columnstore.</span><span class="sxs-lookup"><span data-stu-id="52a61-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="52a61-126">Такое сочетание позволит ускорить для одного набора данных *одновременно* и обработку транзакций, и выполнение аналитических запросов.</span><span class="sxs-lookup"><span data-stu-id="52a61-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="52a61-127">Индексы columnstore и выполняющаяся в памяти OLTP включены в выпуски SQL Server, начиная с версий 2012 и 2014 соответственно.</span><span class="sxs-lookup"><span data-stu-id="52a61-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="52a61-128">Технология обработки в оперативной памяти схожим образом реализована в базе данных SQL Azure и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="52a61-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="52a61-129">При этом новые возможности сначала предоставляются для базы данных SQL Azure, а затем выпускаются для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="52a61-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="52a61-130">В этой статье описываются особенности выполняющейся в памяти OLTP и индексов columnstore, которые применимы только к базе данных SQL Azure. Описание дополняется примерами.</span><span class="sxs-lookup"><span data-stu-id="52a61-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="52a61-131">Сначала мы рассмотрим, как эти технологии влияют на использование хранилища и ограничения размера данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="52a61-132">Вы узнаете, как правильно изменять ценовую категорию для баз данных, в которых используются эти технологии.</span><span class="sxs-lookup"><span data-stu-id="52a61-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="52a61-133">Вы ознакомитесь с двумя примерами по использованию выполняющейся в памяти OLTP и индексов columnstore в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="52a61-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="52a61-134">Для получения дополнительных сведений см. следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="52a61-134">See the following resources for more information.</span></span>

<span data-ttu-id="52a61-135">Ниже приведены ресурсы с более подробными сведениями относительно технологий.</span><span class="sxs-lookup"><span data-stu-id="52a61-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="52a61-136">Статья [Общие сведения и сценарии использования](https://msdn.microsoft.com/library/mt774593.aspx) содержит ссылки на примеры реальных клиентов и сведения, необходимые для начала работы.</span><span class="sxs-lookup"><span data-stu-id="52a61-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="52a61-137">In-Memory OLTP (оптимизация в памяти)</span><span class="sxs-lookup"><span data-stu-id="52a61-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="52a61-138">Описание индексов columnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="52a61-139">Гибридные сценарии транзакционной и аналитической обработки, которые также называются [операционной аналитикой в реальном времени](https://msdn.microsoft.com/library/dn817827.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a61-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="52a61-140">Краткая ознакомительная информация относительно выполняющейся в памяти OLTP: [Краткое руководство 1. Технологии выполнения OLTP в памяти для повышения производительности службы Transact-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (еще одна статья, которая поможет вам приступить к работе).</span><span class="sxs-lookup"><span data-stu-id="52a61-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="52a61-141">Подробные видеоролики об этих технологиях:</span><span class="sxs-lookup"><span data-stu-id="52a61-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="52a61-142">Видеоролик [In-Memory in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (Выполняющаяся в памяти OLTP в базе данных SQL Azure), в котором демонстрируется повышение показателей производительности и описываются шаги для достижения таких же результатов.</span><span class="sxs-lookup"><span data-stu-id="52a61-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- <span data-ttu-id="52a61-143">[In-Memory OLTP Videos: What it is and When/How to use it](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/) (Видео про технологию In-Memory OLTP: что это такое, когда и как ее использовать).</span><span class="sxs-lookup"><span data-stu-id="52a61-143">[In-Memory OLTP Videos: What it is and When/How to use it](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)</span></span>
- <span data-ttu-id="52a61-144">[Columnstore Index: In-Memory Analytics (i.e. columnstore index) Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/) (Видео о выполняющейся в памяти аналитике (например, индексах columnstore) с конференции Ignite 2016).</span><span class="sxs-lookup"><span data-stu-id="52a61-144">[Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)</span></span>

## <a name="storage-and-data-size"></a><span data-ttu-id="52a61-145">Емкость хранилища и объем данных</span><span class="sxs-lookup"><span data-stu-id="52a61-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="52a61-146">Ограничения на объем данных и емкость хранилища для In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="52a61-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="52a61-147">In-Memory OLTP включает оптимизированные для памяти таблицы, которые используются для хранения пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="52a61-148">Эти таблицы должны умещаться в памяти.</span><span class="sxs-lookup"><span data-stu-id="52a61-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="52a61-149">Так как вы управляете памятью непосредственно в службе базы данных SQL, мы применяем концепцию квоты на пользовательские данные,</span><span class="sxs-lookup"><span data-stu-id="52a61-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="52a61-150">или *хранилище выполняющейся в памяти OLTP*.</span><span class="sxs-lookup"><span data-stu-id="52a61-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="52a61-151">Каждая поддерживаемая ценовая категория отдельных баз данных и пулов эластичных баз данных включает некоторый объем хранилища выполняющейся в памяти OLTP.</span><span class="sxs-lookup"><span data-stu-id="52a61-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="52a61-152">На момент написания статьи мы выделяли по 1 ГБ хранилища на каждые 125 единиц транзакций базы данных (DTU) или единиц передачи данных в эластичной базе данных (eDTU).</span><span class="sxs-lookup"><span data-stu-id="52a61-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="52a61-153">В статье [Параметры базы данных SQL и производительность: возможности разных уровней служб](sql-database-service-tiers.md) содержится официальный список объемов хранилища выполняющейся в памяти OLTP, доступный для каждой поддерживаемой ценовой категории отдельных баз данных и пулов эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="52a61-154">При расчете емкости хранилища для выполняющейся в памяти OLTP используются следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="52a61-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="52a61-155">Активные строки пользовательских данных в оптимизированных для памяти таблицах и переменных таблиц.</span><span class="sxs-lookup"><span data-stu-id="52a61-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="52a61-156">Обратите внимание, что старые версии строк не учитываются в объеме.</span><span class="sxs-lookup"><span data-stu-id="52a61-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="52a61-157">Индексы оптимизированных для памяти таблиц.</span><span class="sxs-lookup"><span data-stu-id="52a61-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="52a61-158">Операционные затраты на операции ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="52a61-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="52a61-159">Когда ограничение будет достигнуто, вы получите ошибку с сообщением о том, что квота израсходована, и не сможете выполнять операции вставки и обновления данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="52a61-160">Чтобы устранить такую проблему, удалите часть данных или перейдите на более высокую ценовую категорию базы данных или пула.</span><span class="sxs-lookup"><span data-stu-id="52a61-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="52a61-161">Дополнительные сведения о мониторинге использования хранилища выполняющейся в памяти OLTP и о настройке оповещений при приближении к установленным ограничениям см. в статье [Мониторинг хранилища OLTP в памяти](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="52a61-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="52a61-162">О пулах эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="52a61-162">About elastic pools</span></span>

<span data-ttu-id="52a61-163">При использовании пулов эластичных баз данных хранилище выполняющейся в памяти OLTP используется совместно всеми базами данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="52a61-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="52a61-164">Следовательно, используемый объем одной базы данных может повлиять на другие базы данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="52a61-165">Есть два пути устранения таких проблем.</span><span class="sxs-lookup"><span data-stu-id="52a61-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="52a61-166">Установите для баз данных параметр Max-eDTU ниже, чем значение eDTU для пула в целом.</span><span class="sxs-lookup"><span data-stu-id="52a61-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="52a61-167">Это новое ограничение eDTU на емкость хранилища выполняющейся в памяти OLTP будет действовать в отношении любой базы данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="52a61-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="52a61-168">Установите для баз данных параметр Min-eDTU больше нуля.</span><span class="sxs-lookup"><span data-stu-id="52a61-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="52a61-169">Это минимальное значение гарантирует, что каждая база данных в пуле получит некоторый объем хранилища для выполняющейся в памяти OLTP в соответствии с указанным значением Min-eDTU.</span><span class="sxs-lookup"><span data-stu-id="52a61-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="52a61-170">Размер данных и хранилище для индексов сolumnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="52a61-171">Индексы сolumnstore не обязательно должны помещаться в памяти.</span><span class="sxs-lookup"><span data-stu-id="52a61-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="52a61-172">Поэтому для размера индексов применяется только одно ограничение — на максимальный общий размер базы данных, который описан в статье [Параметры базы данных SQL и производительность: возможности разных уровней служб](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="52a61-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="52a61-173">При использовании кластеризованных индексов сolumnstore для хранения базовых таблиц применяется сжатие по столбцам.</span><span class="sxs-lookup"><span data-stu-id="52a61-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="52a61-174">Сжатие может значительно снизить объем хранимых пользовательских данных, позволяя разместить в базе данных больше информации.</span><span class="sxs-lookup"><span data-stu-id="52a61-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="52a61-175">Этот эффект можно усилить, используя [архивное сжатие по столбцам](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="52a61-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="52a61-176">Степень сжатия, которой можно добиться, зависит от характера данных. Вполне можно достигнуть 10-кратного сжатия.</span><span class="sxs-lookup"><span data-stu-id="52a61-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="52a61-177">Например, если для базы данных установлен максимальный размер 1 терабайт (ТБ), а с помощью технологии columnstore удастся добиться 10-кратного сжатия, вы сможете хранить в этой базе данных 10 ТБ пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="52a61-178">При использовании некластеризованных индексов columnstore базовая таблица по-прежнему хранится в традиционном формате rowstore,</span><span class="sxs-lookup"><span data-stu-id="52a61-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="52a61-179">поэтому экономия места в хранилище будет не столь значительной, как с применением кластеризованных индексов сolumnstore.</span><span class="sxs-lookup"><span data-stu-id="52a61-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="52a61-180">Но если вы при этом замените некоторое число традиционных некластеризованных индексов одним индексом columnstore, даже так вы заметите некоторое сокращение общего объема хранилища для этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="52a61-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="52a61-181">Изменение ценовых категорий баз данных, использующих технологии обработки в оперативной памяти</span><span class="sxs-lookup"><span data-stu-id="52a61-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="52a61-182">При обновлении до более высокой ценовой категории, например со "Стандартной" до "Премиум", не возникнет никаких проблем совместимости или других несоответствий.</span><span class="sxs-lookup"><span data-stu-id="52a61-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="52a61-183">Все доступные функции и ресурсы будут только расширяться.</span><span class="sxs-lookup"><span data-stu-id="52a61-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="52a61-184">Но понижение ценовой категории может отрицательно повлиять на базу данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="52a61-185">Такое влияние при переходе с категории "Премиум" на "Стандартную" или "Базовую" будет особенно заметно, если база данных содержит объекты выполняющейся в памяти OLTP.</span><span class="sxs-lookup"><span data-stu-id="52a61-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="52a61-186">Оптимизированные для памяти таблицы и индексы columnstore станут недоступны после снижения категории (даже если останутся видимыми).</span><span class="sxs-lookup"><span data-stu-id="52a61-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="52a61-187">Эти замечания относятся и к переходу на более низкую ценовую категорию для пула эластичных баз данных, а также к перемещению баз данных, использующих технологии обработки в оперативной памяти, в пул эластичных баз данных уровня "Стандартный" или "Базовый".</span><span class="sxs-lookup"><span data-stu-id="52a61-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="52a61-188">In-Memory OLTP;</span><span class="sxs-lookup"><span data-stu-id="52a61-188">In-Memory OLTP</span></span>

<span data-ttu-id="52a61-189">*Переход на уровни "Базовый" и "Стандартный"*: выполняющаяся в памяти OLTP не поддерживается базами данных уровней "Стандартный" или "Базовый".</span><span class="sxs-lookup"><span data-stu-id="52a61-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="52a61-190">Кроме того, невозможно изменить уровень базы данных, содержащей любые объекты выполняющейся в памяти OLTP, на "Стандартный" или "Базовый".</span><span class="sxs-lookup"><span data-stu-id="52a61-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="52a61-191">Прежде чем понижать базу данных до уровней "Стандартный" или "Базовый", удалите все оптимизированные для памяти таблицы и типы таблиц, а также все модули T-SQL, скомпилированные в собственном коде.</span><span class="sxs-lookup"><span data-stu-id="52a61-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="52a61-192">Вы можете программным методом узнать, поддерживает ли база данных In-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="52a61-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="52a61-193">Для этого выполните следующий запрос Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="52a61-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="52a61-194">Если запрос возвращает **1**, база данных поддерживает In-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="52a61-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="52a61-195">*Понижение до более низкого уровня "Премиум"*: данные в оптимизированных для памяти таблицах должны умещаться в хранилище выполняющейся в памяти OLTP, которое связано с ценовой категорией базы данных или доступно для использования в пуле эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="52a61-196">Если вы попытаетесь понизить ценовую категорию базы данных или переместить базу данных в пул, в котором нет достаточного объема хранилища выполняющейся в памяти OLTP, операция завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="52a61-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="52a61-197">Индексы columnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-197">Columnstore indexes</span></span>

<span data-ttu-id="52a61-198">*Снижение категории до уровня "Стандартный" или "Базовый".* Индексы columnstore поддерживаются только в ценовой категории "Премиум", но не на уровнях "Стандартный" или "Базовый".</span><span class="sxs-lookup"><span data-stu-id="52a61-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="52a61-199">При переходе базы данных на уровень "Стандартный" или "Базовый" индексы columnstore становятся недоступны.</span><span class="sxs-lookup"><span data-stu-id="52a61-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="52a61-200">Система сохранит ваш индекс columnstore, но не будет его использовать.</span><span class="sxs-lookup"><span data-stu-id="52a61-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="52a61-201">Если вы позднее измените ценовую категорию до уровня "Премиум", индекс columnstore будет немедленно готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="52a61-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="52a61-202">Если у вас есть **кластеризованный** индекс columnstore, после понижения уровня вся таблица станет недоступна.</span><span class="sxs-lookup"><span data-stu-id="52a61-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="52a61-203">Поэтому корпорация Майкрософт рекомендует удалить все *кластеризованные* индексы columnstore перед снижением ценовой категории базы данных ниже уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="52a61-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="52a61-204">*Понижение до более низкого уровня "Премиум".* Такая операция пройдет успешно, если общий размер базы данных не превышает максимальный размер хранилища, предусмотренный в новой ценовой категории для баз данных, или доступный в пуле эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="52a61-205">Индексы columnstore особого влияния не оказывают.</span><span class="sxs-lookup"><span data-stu-id="52a61-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="52a61-206">1. Установка образца In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="52a61-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="52a61-207">На [портале Azure](https://portal.azure.com/) вы можете быстро и просто создать пример базы данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="52a61-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="52a61-208">Также в этом разделе объясняется, как можно расширить базу данных AdventureWorksLT с использованием объектов выполняющейся в памяти OLTP, чтобы реализовать повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="52a61-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="52a61-209">Упрощенная, но одновременно более наглядная демонстрация выполняющейся в памяти OLTP представлена здесь:</span><span class="sxs-lookup"><span data-stu-id="52a61-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="52a61-210">Выпуск: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="52a61-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="52a61-211">Исходный код: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="52a61-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="52a61-212">Шаги установки</span><span class="sxs-lookup"><span data-stu-id="52a61-212">Installation steps</span></span>

1. <span data-ttu-id="52a61-213">На [портале Azure](https://portal.azure.com/) создайте базу данных уровня "Премиум" на сервере.</span><span class="sxs-lookup"><span data-stu-id="52a61-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="52a61-214">Укажите **источник** для примера базы данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="52a61-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="52a61-215">Подробные инструкции см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="52a61-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="52a61-216">Подключитесь к базе данных с помощью SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a61-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="52a61-217">Скопируйте в буфер обмена [скрипт Transact-SQL для In-Memory OLTP](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) .</span><span class="sxs-lookup"><span data-stu-id="52a61-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="52a61-218">Скрипт T-SQL создаст необходимые объекты обработки в оперативной памяти в образце базы данных AdventureWorksLT, созданной на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="52a61-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="52a61-219">Вставьте сценарий T-SQL в SSMS, а затем выполните его.</span><span class="sxs-lookup"><span data-stu-id="52a61-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="52a61-220">`MEMORY_OPTIMIZED = ON`Инструкции CREATE TABLE являются ключевыми.</span><span class="sxs-lookup"><span data-stu-id="52a61-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="52a61-221">Например:</span><span class="sxs-lookup"><span data-stu-id="52a61-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="52a61-222">Ошибка 40536</span><span class="sxs-lookup"><span data-stu-id="52a61-222">Error 40536</span></span>


<span data-ttu-id="52a61-223">При запуске скрипта T-SQL может появиться ошибка 40536. В таком случае выполните следующий скрипт T-SQL, чтобы проверить, поддерживает ли база данных компонент In-Memory:</span><span class="sxs-lookup"><span data-stu-id="52a61-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="52a61-224">Значение **0** указывает на то, что обработка в оперативной памяти не поддерживается, а значение **1** — наоборот.</span><span class="sxs-lookup"><span data-stu-id="52a61-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="52a61-225">Чтобы установить причину проблемы, убедитесь, что для базы данных выбран уровень службы "Премиум".</span><span class="sxs-lookup"><span data-stu-id="52a61-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="52a61-226">Сведения о созданных элементах, оптимизированных для памяти</span><span class="sxs-lookup"><span data-stu-id="52a61-226">About the created memory-optimized items</span></span>

<span data-ttu-id="52a61-227">**Таблицы**— пример содержит следующие оптимизированные для памяти таблицы:</span><span class="sxs-lookup"><span data-stu-id="52a61-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="52a61-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="52a61-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="52a61-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="52a61-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="52a61-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="52a61-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="52a61-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="52a61-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="52a61-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="52a61-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="52a61-233">С помощью **обозревателя объектов** в SSMS-файле можно проверить оптимизированные для памяти таблицы.</span><span class="sxs-lookup"><span data-stu-id="52a61-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="52a61-234">Щелкните правой кнопкой мыши **Таблицы** > **Фильтры** > **Параметры фильтров** > **Оптимизирован для памяти**.</span><span class="sxs-lookup"><span data-stu-id="52a61-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="52a61-235">Значение равно 1.</span><span class="sxs-lookup"><span data-stu-id="52a61-235">The value equals 1.</span></span>


<span data-ttu-id="52a61-236">Можно также отправить запрос представлений каталога:</span><span class="sxs-lookup"><span data-stu-id="52a61-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="52a61-237">**Скомпилированная в собственном коде хранимая процедура**: процедуру SalesLT.usp_InsertSalesOrder_inmem можно проверить с помощью запроса представления каталога.</span><span class="sxs-lookup"><span data-stu-id="52a61-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="52a61-238">Запуск образца рабочей нагрузки OLTP</span><span class="sxs-lookup"><span data-stu-id="52a61-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="52a61-239">Единственное различие между двумя следующими *хранимыми процедурами* состоит в том, что первая процедура использует оптимизированные для памяти версии таблиц, а вторая — обычные таблицы на диске:</span><span class="sxs-lookup"><span data-stu-id="52a61-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="52a61-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="52a61-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="52a61-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="52a61-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="52a61-242">В этом разделе описано, как с помощью удобной служебной программы **ostress.exe** можно выполнить две хранимые процедуры в режиме нагрузочного теста.</span><span class="sxs-lookup"><span data-stu-id="52a61-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="52a61-243">При этом вы можете сравнить время выполнения этих нагрузочных тестов.</span><span class="sxs-lookup"><span data-stu-id="52a61-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="52a61-244">При запуске программы ostress.exe рекомендуется передавать значения параметров:</span><span class="sxs-lookup"><span data-stu-id="52a61-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="52a61-245">-n100 — для выполнения большого количества одновременных подключений;</span><span class="sxs-lookup"><span data-stu-id="52a61-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="52a61-246">-r500 — для многократного (сотни раз) выполнения каждого цикла подключения.</span><span class="sxs-lookup"><span data-stu-id="52a61-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="52a61-247">Тем не менее проверку работоспособности можно выполнить и с помощью гораздо меньших значений, например -n10 и -r50.</span><span class="sxs-lookup"><span data-stu-id="52a61-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="52a61-248">Скрипт для ostress.exe</span><span class="sxs-lookup"><span data-stu-id="52a61-248">Script for ostress.exe</span></span>


<span data-ttu-id="52a61-249">В этом разделе приведен скрипт T-SQL, внедренный в командную строку ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="52a61-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="52a61-250">Этот скрипт использует элементы, созданные ранее с помощью установленного скрипта T-SQL.</span><span class="sxs-lookup"><span data-stu-id="52a61-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="52a61-251">Следующий скрипт вставляет образец заказа на продажу с пятью позициями строки в следующие оптимизированные для памяти *таблицы*:</span><span class="sxs-lookup"><span data-stu-id="52a61-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="52a61-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="52a61-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="52a61-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="52a61-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="52a61-254">Чтобы создать версию представленного выше скрипта T-SQL для ostress.exe для таблиц *на диске*, измените оба вхождения подстроки *_inmem* на *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="52a61-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="52a61-255">Эти замены влияют на имена таблиц и хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="52a61-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="52a61-256">Установка служебных программ RML и ostress</span><span class="sxs-lookup"><span data-stu-id="52a61-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="52a61-257">В идеале вам следует запланировать запуск ostress.exe на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="52a61-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="52a61-258">Вам нужно создать [виртуальную машину Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) в том же географическом регионе Azure, в котором находится база данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="52a61-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="52a61-259">Но вы также можете запустить программу ostress.exe и на переносном компьютере.</span><span class="sxs-lookup"><span data-stu-id="52a61-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="52a61-260">На виртуальной машине (или в другом размещении) установите служебные программы RML,</span><span class="sxs-lookup"><span data-stu-id="52a61-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="52a61-261">которые включают в себя ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="52a61-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="52a61-262">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="52a61-262">For more information, see:</span></span>
- <span data-ttu-id="52a61-263">Обсуждение программы ostress.exe представлено в статье [Пример базы данных для выполняющейся в памяти OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a61-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="52a61-264">Или ознакомьтесь со статьей [Пример базы данных для выполняющейся в памяти OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a61-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="52a61-265">Можно также прочитать [блог об установке ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a61-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="52a61-266">Запуск тестовой рабочей нагрузки *_inmem*</span><span class="sxs-lookup"><span data-stu-id="52a61-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="52a61-267">Вы можете использовать окно *командной строки RML* , чтобы запустить командную строку ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="52a61-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="52a61-268">Параметры командной строки указывают программе ostress выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="52a61-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="52a61-269">параллельно выполнять 100 подключений (-n100);</span><span class="sxs-lookup"><span data-stu-id="52a61-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="52a61-270">заставлять каждое подключение запускать сценарий T-SQL 50 раз (-r50).</span><span class="sxs-lookup"><span data-stu-id="52a61-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="52a61-271">Выполнить предыдущую команду ostress.exe можно так.</span><span class="sxs-lookup"><span data-stu-id="52a61-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="52a61-272">Чтобы удалить все данные, вставленные в ходе предыдущих запусков, сбросьте содержимое базы данных, выполнив следующую команду в SSMS.</span><span class="sxs-lookup"><span data-stu-id="52a61-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="52a61-273">Скопируйте текст предыдущей командной строки ostress.exe в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="52a61-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="52a61-274">Замените `<placeholders>` для параметров -S, -U, -P, и -d правильными фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="52a61-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="52a61-275">В окне командной строки RML запустите измененную командную строку.</span><span class="sxs-lookup"><span data-stu-id="52a61-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="52a61-276">Результат — это длительность выполнения теста</span><span class="sxs-lookup"><span data-stu-id="52a61-276">Result is a duration</span></span>


<span data-ttu-id="52a61-277">При завершении программа ostress.exe записывает значение длительности выполнения в последней строке выходных данных в окне командной строки RML.</span><span class="sxs-lookup"><span data-stu-id="52a61-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="52a61-278">Например, более короткий тестовый запуск длится около 1,5 минут:</span><span class="sxs-lookup"><span data-stu-id="52a61-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="52a61-279">Сброс базы данных, изменение значения *_ondisk* и повторный запуск</span><span class="sxs-lookup"><span data-stu-id="52a61-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="52a61-280">Получив результат выполнения *_inmem*, выполните следующие действия для запуска *_ondisk*:</span><span class="sxs-lookup"><span data-stu-id="52a61-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="52a61-281">Выполните сброс базы данных, запустив следующую команду в SSMS. Она удалит все данные, вставленные в ходе предыдущего запуска.</span><span class="sxs-lookup"><span data-stu-id="52a61-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="52a61-282">Измените командную строку ostress.exe, заменив все вхождения *_inmem* на *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="52a61-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="52a61-283">Перезапустите ostress.exe еще раз и запишите результат (длительность выполнения).</span><span class="sxs-lookup"><span data-stu-id="52a61-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="52a61-284">Еще раз выполните сброс базы данных, чтобы корректно удалить большой объем тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="52a61-285">Ожидаемые результаты сравнения</span><span class="sxs-lookup"><span data-stu-id="52a61-285">Expected comparison results</span></span>

<span data-ttu-id="52a61-286">Выполняющиеся в памяти тесты демонстрируют **9-кратное** повышение производительности для упрощенных рабочих нагрузок. При этом программа ostress выполняется на виртуальной машине Azure, расположенной в том же регионе Azure, что и база данных.</span><span class="sxs-lookup"><span data-stu-id="52a61-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="52a61-287">2) Установка образца In-Memory Analytics</span><span class="sxs-lookup"><span data-stu-id="52a61-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="52a61-288">В этом разделе вы сравните результаты ввода-вывода и статистические данные при использовании индекса columnstore и традиционного индекса сбалансированного дерева.</span><span class="sxs-lookup"><span data-stu-id="52a61-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="52a61-289">Для анализа в режиме реального времени с использованием рабочей нагрузки OLTP зачастую лучше использовать некластеризованный индекс columnstore.</span><span class="sxs-lookup"><span data-stu-id="52a61-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="52a61-290">Дополнительные сведения см. в статье [Руководство по индексам columnstore](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a61-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="52a61-291">Подготовка тестирования аналитики с помощью columnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="52a61-292">С помощью портала Azure создайте из образца новую базу данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="52a61-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="52a61-293">Используйте такое же имя.</span><span class="sxs-lookup"><span data-stu-id="52a61-293">Use that exact name.</span></span>
 - <span data-ttu-id="52a61-294">Выберите любой уровень служб категории «Премиум».</span><span class="sxs-lookup"><span data-stu-id="52a61-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="52a61-295">Скопируйте [sql_inmemory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="52a61-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="52a61-296">Скрипт T-SQL создаст необходимые объекты обработки в оперативной памяти в образце базы данных AdventureWorksLT, созданной на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="52a61-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="52a61-297">Скрипт создаст таблицу измерений и две таблицы фактов.</span><span class="sxs-lookup"><span data-stu-id="52a61-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="52a61-298">Таблицы фактов заполняются 3,5 млн строк.</span><span class="sxs-lookup"><span data-stu-id="52a61-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="52a61-299">Выполнение скрипта может занять до 15 минут.</span><span class="sxs-lookup"><span data-stu-id="52a61-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="52a61-300">Вставьте сценарий T-SQL в SSMS, а затем выполните его.</span><span class="sxs-lookup"><span data-stu-id="52a61-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="52a61-301">Важным является ключевое слово **COLUMNSTORE** в инструкции **CREATE INDEX**, как и в:</span><span class="sxs-lookup"><span data-stu-id="52a61-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="52a61-302">Задайте для базы данных AdventureWorksLT уровень совместимости 130:</span><span class="sxs-lookup"><span data-stu-id="52a61-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="52a61-303">Уровень 130 не имеет прямого отношения к компонентам In-Memory.</span><span class="sxs-lookup"><span data-stu-id="52a61-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="52a61-304">При этом уровень 130 обычно обеспечивает более высокую скорость обработки запросов, чем уровень 120.</span><span class="sxs-lookup"><span data-stu-id="52a61-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="52a61-305">Ключевые таблицы и индексы columnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="52a61-306">dbo.FactResellerSalesXL_CCI — это таблица, включающая в себя кластеризованный индекс columnstore с дополнительными возможностями сжатия на уровне *данных*.</span><span class="sxs-lookup"><span data-stu-id="52a61-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="52a61-307">dbo.FactResellerSalesXL_PageCompressed — это таблица с эквивалентным обычным кластеризованным индексом, который сжат только на уровне *страницы*.</span><span class="sxs-lookup"><span data-stu-id="52a61-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="52a61-308">Ключевые запросы для сравнения с индексом columnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="52a61-309">Существует [несколько типов запросов T-SQL, которые можно выполнить](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) для анализа повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="52a61-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="52a61-310">На втором шаге скрипта T-SQL обратите внимание на следующую пару запросов.</span><span class="sxs-lookup"><span data-stu-id="52a61-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="52a61-311">Они отличаются только одной строкой.</span><span class="sxs-lookup"><span data-stu-id="52a61-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="52a61-312">Кластеризованный индекс columnstore включен в таблицу FactResellerSalesXL\_CCI.</span><span class="sxs-lookup"><span data-stu-id="52a61-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="52a61-313">Следующий фрагмент скрипта T-SQL отображает статистику для ввода-вывода, а также время выполнения запроса (TIME) для каждой таблицы.</span><span class="sxs-lookup"><span data-stu-id="52a61-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
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


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
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

<span data-ttu-id="52a61-314">При использовании кластеризованного индекса рост производительности для этого запроса в базе данных ценовой категории P2 может увеличиться примерно в 9 раз по сравнению с традиционным индексом.</span><span class="sxs-lookup"><span data-stu-id="52a61-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="52a61-315">При использовании кластеризованного индекса в базе данных ценовой категории P15 можно ожидать рост производительности примерно в 57 раз.</span><span class="sxs-lookup"><span data-stu-id="52a61-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="52a61-316">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52a61-316">Next steps</span></span>

- [<span data-ttu-id="52a61-317">Краткое руководство 1. Технологии выполнения OLTP в памяти для повышения производительности службы Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="52a61-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="52a61-318">Повышение производительности приложений в базе данных SQL с помощью выполняющейся в памяти OLTP</span><span class="sxs-lookup"><span data-stu-id="52a61-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="52a61-319">[Мониторинг хранилища OLTP в памяти](sql-database-in-memory-oltp-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="52a61-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="52a61-320">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="52a61-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="52a61-321">Подробные сведения</span><span class="sxs-lookup"><span data-stu-id="52a61-321">Deeper information</span></span>

- <span data-ttu-id="52a61-322">Узнайте, как [Quorum удваивает ключевую рабочую нагрузку на базу данных при одновременном сокращении DTU на 70 % благодаря использованию In-Memory OLTP для базы данных SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="52a61-322">[Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>

- <span data-ttu-id="52a61-323">[In-Memory OLTP in Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Выполняющаяся в памяти OLTP в базе данных SQL Azure)</span><span class="sxs-lookup"><span data-stu-id="52a61-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

- <span data-ttu-id="52a61-324">[Learn about In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx) (Знакомство с In-Memory OLTP)</span><span class="sxs-lookup"><span data-stu-id="52a61-324">[Learn about In-Memory OLTP](http://msdn.microsoft.com/library/dn133186.aspx)</span></span>

- [<span data-ttu-id="52a61-325">Руководство по индексам columnstore</span><span class="sxs-lookup"><span data-stu-id="52a61-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="52a61-326">Начало работы с Columnstore для получения операционной аналитики в реальном времени</span><span class="sxs-lookup"><span data-stu-id="52a61-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="52a61-327">Технический документ с [рекомендациями по распространенным шаблонам рабочих нагрузок и миграции](http://msdn.microsoft.com/library/dn673538.aspx) включает описание шаблонов рабочих нагрузок, для которых выполняющаяся OLTP обычно обеспечивает значительное повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="52a61-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="52a61-328">Проектирование приложений</span><span class="sxs-lookup"><span data-stu-id="52a61-328">Application design</span></span>

- [<span data-ttu-id="52a61-329">In-Memory OLTP (оптимизация в памяти)</span><span class="sxs-lookup"><span data-stu-id="52a61-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="52a61-330">Повышение производительности приложений в базе данных SQL с помощью выполняющейся в памяти OLTP</span><span class="sxs-lookup"><span data-stu-id="52a61-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="52a61-331">Средства</span><span class="sxs-lookup"><span data-stu-id="52a61-331">Tools</span></span>

- [<span data-ttu-id="52a61-332">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="52a61-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="52a61-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="52a61-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="52a61-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="52a61-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
