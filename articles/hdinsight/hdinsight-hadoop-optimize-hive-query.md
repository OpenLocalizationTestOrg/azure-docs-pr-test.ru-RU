---
title: "запросы aaaOptimize Hive в Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toooptimize вашей Hive запрашивает Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="7c39c-103">Оптимизация запросов Hive в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c39c-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="7c39c-104">По умолчанию производительность кластеров Hadoop не оптимизирована.</span><span class="sxs-lookup"><span data-stu-id="7c39c-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="7c39c-105">В этой статье описываются некоторые наиболее распространенные Hive производительности оптимизации методы, могут быть применены tooyour запросов.</span><span class="sxs-lookup"><span data-stu-id="7c39c-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="7c39c-106">Горизонтальное масштабирование рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="7c39c-106">Scale out worker nodes</span></span>

<span data-ttu-id="7c39c-107">При увеличении числа hello рабочих узлов в кластере могут использовать дополнительные модули сопоставления и reducers toobe параллельного выполнения.</span><span class="sxs-lookup"><span data-stu-id="7c39c-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="7c39c-108">Горизонтальное масштабирование в HDInsight можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="7c39c-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="7c39c-109">Во время подготовки hello можно указать hello число рабочих узлов, используя hello портал Azure, Azure PowerShell или межплатформенного интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="7c39c-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="7c39c-110">Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7c39c-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="7c39c-111">Hello следующем снимке экрана показан рабочий hello конфигурации узла на портал Azure hello:</span><span class="sxs-lookup"><span data-stu-id="7c39c-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="7c39c-113">Во время выполнения hello можно масштабировать кластер без повторного создания один:</span><span class="sxs-lookup"><span data-stu-id="7c39c-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="7c39c-115">Дополнительные сведения о разных виртуальных машин hello поддерживается HDInsight см. в разделе [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7c39c-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="7c39c-116">Включение Tez</span><span class="sxs-lookup"><span data-stu-id="7c39c-116">Enable Tez</span></span>

<span data-ttu-id="7c39c-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) — это ядро MapReduce альтернативных выполнения toohello ядра:</span><span class="sxs-lookup"><span data-stu-id="7c39c-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="7c39c-119">Tez работает быстрее, так как:</span><span class="sxs-lookup"><span data-stu-id="7c39c-119">Tez is faster because:</span></span>

* <span data-ttu-id="7c39c-120">**Выполнение направленный ациклического графа (DAG) как единое задание MapReduce ядра hello**.</span><span class="sxs-lookup"><span data-stu-id="7c39c-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="7c39c-121">Hello DAG требует каждого набора следуют один набор reducers toobe модули сопоставления.</span><span class="sxs-lookup"><span data-stu-id="7c39c-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="7c39c-122">В этом случае несколько toobe заданий MapReduce, она появится для каждого запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="7c39c-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="7c39c-123">Tez не имеет такого ограничения и может обрабатывать сложные DAG как единое задание, тем самым  сводя к минимуму затраты на создание новых заданий.</span><span class="sxs-lookup"><span data-stu-id="7c39c-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="7c39c-124">**Позволяет избежать ненужных операций записи.**</span><span class="sxs-lookup"><span data-stu-id="7c39c-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="7c39c-125">Из-за toomultiple заданий она появится для hello того же запроса Hive подсистемы hello MapReduce, выходные данные каждого задания hello записывается tooHDFS для промежуточных данных.</span><span class="sxs-lookup"><span data-stu-id="7c39c-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="7c39c-126">Поскольку Tez сводит к минимуму количество заданий для каждого запроса Hive, она будет может tooavoid ненужные записи.</span><span class="sxs-lookup"><span data-stu-id="7c39c-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="7c39c-127">**Сводит к минимуму задержки при загрузке.**</span><span class="sxs-lookup"><span data-stu-id="7c39c-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="7c39c-128">Tez — более высокую задержку при запуске может toominimize за счет сокращения числа hello модули сопоставления, необходимые toostart, а также улучшение оптимизацию во всей.</span><span class="sxs-lookup"><span data-stu-id="7c39c-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="7c39c-129">**Повторно использует контейнеры.**</span><span class="sxs-lookup"><span data-stu-id="7c39c-129">**Reuses containers**.</span></span> <span data-ttu-id="7c39c-130">Всякий раз, когда возможно Tez tooensure контейнеры могут tooreuse этой задержки из-за toostarting копирование контейнеры уменьшается.</span><span class="sxs-lookup"><span data-stu-id="7c39c-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="7c39c-131">**Применяет методы непрерывной оптимизации.**</span><span class="sxs-lookup"><span data-stu-id="7c39c-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="7c39c-132">Традиционно оптимизация выполняется на этапе компиляции.</span><span class="sxs-lookup"><span data-stu-id="7c39c-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="7c39c-133">Однако можно найти дополнительные сведения о входных атрибутах hello, позволяющие лучше оптимизации во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="7c39c-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="7c39c-134">Tez используются методы непрерывной оптимизации, которые позволяет toooptimize дальнейшей hello плана на этап выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="7c39c-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="7c39c-135">Дополнительные сведения об этих понятиях см. в документе об [Apache Tez](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="7c39c-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="7c39c-136">Можно выбрать любой запрос Hive Tez включена с помощью префикса hello запроса с параметром hello ниже:</span><span class="sxs-lookup"><span data-stu-id="7c39c-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="7c39c-137">При подготовке кластеров HDInsight под управлением Linux платформа Tez включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7c39c-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="7c39c-138">Секционирование данных в Hive</span><span class="sxs-lookup"><span data-stu-id="7c39c-138">Hive partitioning</span></span>

<span data-ttu-id="7c39c-139">Операции ввода-вывода является узким местом производительности основных hello для выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="7c39c-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="7c39c-140">Hello производительность можно повысить, если hello объем данных, которые должны toobe прочитать может быть уменьшен.</span><span class="sxs-lookup"><span data-stu-id="7c39c-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="7c39c-141">По умолчанию запросы Hive просматривают все таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="7c39c-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="7c39c-142">Это очень удобно для запросов, выполняющих сканирование таблиц.</span><span class="sxs-lookup"><span data-stu-id="7c39c-142">This is great for queries like table scans.</span></span> <span data-ttu-id="7c39c-143">Однако для запросов, которым требуется только tooscan небольшой объем данных (например, запросы с фильтрацией), это поведение создает ненужные затраты.</span><span class="sxs-lookup"><span data-stu-id="7c39c-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="7c39c-144">Куст секционирование позволяет Hive запросы tooaccess только hello необходимые объем данных в таблицах Hive.</span><span class="sxs-lookup"><span data-stu-id="7c39c-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="7c39c-145">Секционирование Hive реализуется путем реорганизации hello необработанных данных в новые каталоги с каждой секцией, имеющих свой собственный каталог - где определена секция hello пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="7c39c-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="7c39c-146">Hello следующая схема иллюстрирует секционирование таблицу Hive по столбцу hello *год*.</span><span class="sxs-lookup"><span data-stu-id="7c39c-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="7c39c-147">Для каждого года создается новый каталог.</span><span class="sxs-lookup"><span data-stu-id="7c39c-147">A new directory is created for each year.</span></span>

![Секционирование][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="7c39c-149">Некоторые рекомендации для выполнения секционирования:</span><span class="sxs-lookup"><span data-stu-id="7c39c-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="7c39c-150">**Секций не должно быть слишком мало.** Секционирование по столбцам, содержащим только небольшое количество значений, может привести к малому количеству секций.</span><span class="sxs-lookup"><span data-stu-id="7c39c-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="7c39c-151">Например, только секционирование по полу создает два toobe секции, созданные (Мужской» и «Женский), таким образом только уменьшить задержку hello, более половины.</span><span class="sxs-lookup"><span data-stu-id="7c39c-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="7c39c-152">**Не увеличивайте секции** : В Здравствуйте другой стороны, Создание секции для столбца с уникальным значением (например, userid) вызывает несколько секций.</span><span class="sxs-lookup"><span data-stu-id="7c39c-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="7c39c-153">Через секции вызывает объем нагрузки namenode hello кластера как с toohandle hello большое количество папок.</span><span class="sxs-lookup"><span data-stu-id="7c39c-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="7c39c-154">**Избегайте неравномерного распределения данных** — выбирайте ключ секционирования рационально, таким образом, чтобы все секции были одинакового размера.</span><span class="sxs-lookup"><span data-stu-id="7c39c-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="7c39c-155">Примером является секционирования на *состояние* может привести к hello число записей в Калифорнии toobe почти 30 x, Вермонт из-за разницы toohello в совокупности.</span><span class="sxs-lookup"><span data-stu-id="7c39c-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="7c39c-156">toocreate секции таблицы, используйте hello *секционированы по* предложения:</span><span class="sxs-lookup"><span data-stu-id="7c39c-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="7c39c-157">После создания секционированной таблицы hello, можно создать статическое разделение или динамическое секционирование.</span><span class="sxs-lookup"><span data-stu-id="7c39c-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="7c39c-158">**Статическое разделение** означает, что имеется уже сегментированных данных в hello соответствующими каталоги и вы можете запросить Hive секций вручную по расположение каталога hello.</span><span class="sxs-lookup"><span data-stu-id="7c39c-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="7c39c-159">Следующий фрагмент кода Hello приведен пример.</span><span class="sxs-lookup"><span data-stu-id="7c39c-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="7c39c-160">**Динамическое секционирование** означает потребность автоматически куст toocreate секций для вас.</span><span class="sxs-lookup"><span data-stu-id="7c39c-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="7c39c-161">Так как мы уже создали hello секционирование таблицы из промежуточной таблицы hello, нам нужно toodo всего таблицы секционированы toohello вставки данных:</span><span class="sxs-lookup"><span data-stu-id="7c39c-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="7c39c-162">Для получения дополнительных сведений обратитесь к разделу [Секционированные таблицы](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="7c39c-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="7c39c-163">Используйте формат ORCFile hello</span><span class="sxs-lookup"><span data-stu-id="7c39c-163">Use hello ORCFile format</span></span>
<span data-ttu-id="7c39c-164">Hive поддерживает различные форматы.</span><span class="sxs-lookup"><span data-stu-id="7c39c-164">Hive supports different file formats.</span></span> <span data-ttu-id="7c39c-165">Например:</span><span class="sxs-lookup"><span data-stu-id="7c39c-165">For example:</span></span>

* <span data-ttu-id="7c39c-166">**Текст**: это формат файла по умолчанию hello и работает с большинство сценариев</span><span class="sxs-lookup"><span data-stu-id="7c39c-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="7c39c-167">**Avro**: хорошо подходит для сценариев взаимодействия</span><span class="sxs-lookup"><span data-stu-id="7c39c-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="7c39c-168">**ORC/Parquet**: лучше всего подходит для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="7c39c-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="7c39c-169">Формат ORC (оптимизированный строк по столбцам) является очень эффективным способом toostore данных Hive.</span><span class="sxs-lookup"><span data-stu-id="7c39c-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="7c39c-170">Форматы сравниваемых tooother, ORC имеет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7c39c-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="7c39c-171">поддержка сложных типов, включая даты и время и частично структурированные и сложные типы</span><span class="sxs-lookup"><span data-stu-id="7c39c-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="7c39c-172">Сжатие % too70</span><span class="sxs-lookup"><span data-stu-id="7c39c-172">up too70% compression</span></span>
* <span data-ttu-id="7c39c-173">индексирует каждые 10 000 строк, что позволяет пропускать строки;</span><span class="sxs-lookup"><span data-stu-id="7c39c-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="7c39c-174">обеспечивает существенное снижение времени выполнения запросов</span><span class="sxs-lookup"><span data-stu-id="7c39c-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="7c39c-175">Формат ORC tooenable, то сначала нужно создать таблицу с предложением hello *хранятся в виде ORC*:</span><span class="sxs-lookup"><span data-stu-id="7c39c-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="7c39c-176">Затем можно вставить таблицу ORC toohello данных из hello, Промежуточная таблица.</span><span class="sxs-lookup"><span data-stu-id="7c39c-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="7c39c-177">Например:</span><span class="sxs-lookup"><span data-stu-id="7c39c-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="7c39c-178">Вы можете прочитать больше на формат ORC hello [здесь](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="7c39c-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="7c39c-179">Векторизация</span><span class="sxs-lookup"><span data-stu-id="7c39c-179">Vectorization</span></span>

<span data-ttu-id="7c39c-180">Векторизации позволяет куст tooprocess пакет 1024 вместе строк вместо обработки одной строке за раз.</span><span class="sxs-lookup"><span data-stu-id="7c39c-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="7c39c-181">Это означает, что простые операции выполняются быстрее, так как toorun требуется меньше внутреннего кода.</span><span class="sxs-lookup"><span data-stu-id="7c39c-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="7c39c-182">запрос Hive векторизации tooenable префикс hello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="7c39c-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="7c39c-183">Для получения дополнительных сведений обратитесь к разделу [Выполнение векторизованного запроса](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="7c39c-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="7c39c-184">Другие методы оптимизации</span><span class="sxs-lookup"><span data-stu-id="7c39c-184">Other optimization methods</span></span>
<span data-ttu-id="7c39c-185">Существуют дополнительные методы оптимизации, которые также можно использовать, например:</span><span class="sxs-lookup"><span data-stu-id="7c39c-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="7c39c-186">**Куст сегментацию:** технику, которая позволяет больших наборов данных производительности запросов toooptimize toocluster или сегмента.</span><span class="sxs-lookup"><span data-stu-id="7c39c-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="7c39c-187">**Оптимизации соединения:** оптимизации выполнения запроса Hive планирование tooimprove hello эффективности соединений и уменьшают затраты hello указаний пользователя.</span><span class="sxs-lookup"><span data-stu-id="7c39c-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="7c39c-188">Для получения дополнительных сведений обратитесь к разделу [Оптимизация объединений](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="7c39c-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="7c39c-189">**Увеличение модулей сжатия.**</span><span class="sxs-lookup"><span data-stu-id="7c39c-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c39c-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c39c-190">Next steps</span></span>
<span data-ttu-id="7c39c-191">В этой статье вы узнали некоторые распространенные методы оптимизации запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="7c39c-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="7c39c-192">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="7c39c-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="7c39c-193">Использование Apache Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c39c-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7c39c-194">Анализ данных о задержке рейсов с помощью Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c39c-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="7c39c-195">Анализ данных Twitter с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c39c-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="7c39c-196">Анализ данных датчика с помощью hello Hive консоль запросов в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c39c-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="7c39c-197">Используйте Hive в HDInsight tooanalyze журналы веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="7c39c-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
