---
title: "Оптимизация запросов Hive в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как оптимизировать запросы Hive для Hadoop в HDInsight."
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
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="5a30d-103">Оптимизация запросов Hive в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a30d-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="5a30d-104">По умолчанию производительность кластеров Hadoop не оптимизирована.</span><span class="sxs-lookup"><span data-stu-id="5a30d-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="5a30d-105">В этой статье описывается несколько наиболее распространенных методов оптимизации производительности Hive, которые можно применить к отправке запросов.</span><span class="sxs-lookup"><span data-stu-id="5a30d-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="5a30d-106">Горизонтальное масштабирование рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="5a30d-106">Scale out worker nodes</span></span>

<span data-ttu-id="5a30d-107">Увеличение числа рабочих узлов в кластере может дать возможность большему числу модулей сопоставления и сжатия работать параллельно.</span><span class="sxs-lookup"><span data-stu-id="5a30d-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="5a30d-108">Горизонтальное масштабирование в HDInsight можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="5a30d-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="5a30d-109">Во время подготовки можно указать количество рабочих узлов при помощи портала Azure, Azure PowerShell или кроссплатформенного интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="5a30d-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="5a30d-110">Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5a30d-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="5a30d-111">На следующем снимке экрана показана рабочая конфигурация узла на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="5a30d-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="5a30d-113">Во время выполнения можно масштабировать кластер без необходимости его повторного создания.</span><span class="sxs-lookup"><span data-stu-id="5a30d-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="5a30d-115">Дополнительные сведения о разных виртуальных машинах, поддерживаемых HDInsight, см. на странице [цен на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5a30d-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="5a30d-116">Включение Tez</span><span class="sxs-lookup"><span data-stu-id="5a30d-116">Enable Tez</span></span>

<span data-ttu-id="5a30d-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) — это механизм выполнения, альтернативный механизму MapReduce:</span><span class="sxs-lookup"><span data-stu-id="5a30d-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="5a30d-119">Tez работает быстрее, так как:</span><span class="sxs-lookup"><span data-stu-id="5a30d-119">Tez is faster because:</span></span>

* <span data-ttu-id="5a30d-120">**Выполняет задания, представленные в виде направленных ациклических графов (DAG), как единое целое при работе с платформой MapReduce.**</span><span class="sxs-lookup"><span data-stu-id="5a30d-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="5a30d-121">DAG требует, чтобы набору модулей сопоставления соответствовал набор модулей сжатия.</span><span class="sxs-lookup"><span data-stu-id="5a30d-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="5a30d-122">Это приводит к созданию множества заданий MapReduce для каждого запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="5a30d-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="5a30d-123">Tez не имеет такого ограничения и может обрабатывать сложные DAG как единое задание, тем самым  сводя к минимуму затраты на создание новых заданий.</span><span class="sxs-lookup"><span data-stu-id="5a30d-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="5a30d-124">**Позволяет избежать ненужных операций записи.**</span><span class="sxs-lookup"><span data-stu-id="5a30d-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="5a30d-125">Из-за возникновения многочисленных заданий для каждого запроса Hive при работе на платформе MapReduce, результат каждого задания записывается в HDFS в качестве промежуточных данных.</span><span class="sxs-lookup"><span data-stu-id="5a30d-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="5a30d-126">Поскольку Tez сводит к минимуму количество заданий для каждого запроса Hive, это позволяет избежать ненужных операций записи.</span><span class="sxs-lookup"><span data-stu-id="5a30d-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="5a30d-127">**Сводит к минимуму задержки при загрузке.**</span><span class="sxs-lookup"><span data-stu-id="5a30d-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="5a30d-128">Платформа Tez способствует снижению задержки при запуске благодаря уменьшению количества модулей сопоставления, необходимых для запуска, а также путем оптимизации всего процесса.</span><span class="sxs-lookup"><span data-stu-id="5a30d-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="5a30d-129">**Повторно использует контейнеры.**</span><span class="sxs-lookup"><span data-stu-id="5a30d-129">**Reuses containers**.</span></span> <span data-ttu-id="5a30d-130">Каждый раз, когда появляется возможность, Tez повторно использует контейнеры, таким образом снижая задержки при запуске контейнеров.</span><span class="sxs-lookup"><span data-stu-id="5a30d-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="5a30d-131">**Применяет методы непрерывной оптимизации.**</span><span class="sxs-lookup"><span data-stu-id="5a30d-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="5a30d-132">Традиционно оптимизация выполняется на этапе компиляции.</span><span class="sxs-lookup"><span data-stu-id="5a30d-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="5a30d-133">Однако по мере поступления дополнительных сведений о входных данных появляется возможность улучшить оптимизацию уже на этапе работы.</span><span class="sxs-lookup"><span data-stu-id="5a30d-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="5a30d-134">Tez применяет методы непрерывной оптимизации, что позволяет производить дальнейшую оптимизацию плана на этапе работы.</span><span class="sxs-lookup"><span data-stu-id="5a30d-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="5a30d-135">Дополнительные сведения об этих понятиях см. в документе об [Apache Tez](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="5a30d-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="5a30d-136">Вы можете выполнить любой запрос Hive, используя платформу Tez, активировав ее с помощью префикса запроса со следующими параметрам:</span><span class="sxs-lookup"><span data-stu-id="5a30d-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="5a30d-137">При подготовке кластеров HDInsight под управлением Linux платформа Tez включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5a30d-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="5a30d-138">Секционирование данных в Hive</span><span class="sxs-lookup"><span data-stu-id="5a30d-138">Hive partitioning</span></span>

<span data-ttu-id="5a30d-139">Операция ввода-вывода — это основной ограничивающий фактор производительности при выполнении запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="5a30d-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="5a30d-140">Производительность можно повысить, если удастся уменьшить объем данных, которые необходимо считать.</span><span class="sxs-lookup"><span data-stu-id="5a30d-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="5a30d-141">По умолчанию запросы Hive просматривают все таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="5a30d-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="5a30d-142">Это очень удобно для запросов, выполняющих сканирование таблиц.</span><span class="sxs-lookup"><span data-stu-id="5a30d-142">This is great for queries like table scans.</span></span> <span data-ttu-id="5a30d-143">Однако для запросов, которым требуется просмотреть только небольшой объем данных (например, для запросов с фильтрацией), это поведение создает излишнюю нагрузку.</span><span class="sxs-lookup"><span data-stu-id="5a30d-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="5a30d-144">Секционирование данных Hive предоставляет запросам Hive доступ только к необходимому объему данных в таблицах Hive.</span><span class="sxs-lookup"><span data-stu-id="5a30d-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="5a30d-145">Секционирование данных Hive реализуется путем реорганизации необработанных данных в новые каталоги с присвоением каждой секции своего собственного каталога, где секция определяется пользователем.</span><span class="sxs-lookup"><span data-stu-id="5a30d-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="5a30d-146">Следующая схема иллюстрирует секционирование таблицы Hive по столбцу *Год*.</span><span class="sxs-lookup"><span data-stu-id="5a30d-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="5a30d-147">Для каждого года создается новый каталог.</span><span class="sxs-lookup"><span data-stu-id="5a30d-147">A new directory is created for each year.</span></span>

![Секционирование][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="5a30d-149">Некоторые рекомендации для выполнения секционирования:</span><span class="sxs-lookup"><span data-stu-id="5a30d-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="5a30d-150">**Секций не должно быть слишком мало.** Секционирование по столбцам, содержащим только небольшое количество значений, может привести к малому количеству секций.</span><span class="sxs-lookup"><span data-stu-id="5a30d-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="5a30d-151">Например, секционирование по половой принадлежности создает только две секции ("Мужская" и "Женская"), тем самым это сокращает задержку только наполовину.</span><span class="sxs-lookup"><span data-stu-id="5a30d-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="5a30d-152">**Секций не должно быть слишком много.** С другой стороны, создание секции для столбца с уникальным значением (например, содержащим идентификатор пользователя userid) приведет к появлению множества секций,</span><span class="sxs-lookup"><span data-stu-id="5a30d-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="5a30d-153">что увеличит нагрузку на узел имен кластера из-за необходимости обрабатывать множество каталогов.</span><span class="sxs-lookup"><span data-stu-id="5a30d-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="5a30d-154">**Избегайте неравномерного распределения данных** — выбирайте ключ секционирования рационально, таким образом, чтобы все секции были одинакового размера.</span><span class="sxs-lookup"><span data-stu-id="5a30d-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="5a30d-155">Например секционирование по *Штату* может привести к тому, что количество записей по Калифорнии будет почти в 30 раз больше, чем для Вермонта, из-за различия в населении штатов.</span><span class="sxs-lookup"><span data-stu-id="5a30d-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="5a30d-156">Чтобы выполнить секционирование таблицы, используйте команду *Секционирована по* :</span><span class="sxs-lookup"><span data-stu-id="5a30d-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="5a30d-157">Как только секционированная таблица будет создана, можно выполнить статическое или динамическое секционирование.</span><span class="sxs-lookup"><span data-stu-id="5a30d-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="5a30d-158">**Статическое секционирование** означает, что вы уже распределили данные по соответствующим каталогам и можете выполнить создание секций Hive вручную, исходя из расположения каталогов.</span><span class="sxs-lookup"><span data-stu-id="5a30d-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="5a30d-159">Просмотрите пример в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="5a30d-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="5a30d-160">**Динамическое секционирование** означает, что Hive автоматически создаст секции для вас.</span><span class="sxs-lookup"><span data-stu-id="5a30d-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="5a30d-161">Так как таблица секционирования уже была создана из промежуточной таблицы, теперь достаточно только выполнить вставку данных в секционированную таблицу:</span><span class="sxs-lookup"><span data-stu-id="5a30d-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="5a30d-162">Для получения дополнительных сведений обратитесь к разделу [Секционированные таблицы](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="5a30d-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="5a30d-163">Использование формата ORC-файлов</span><span class="sxs-lookup"><span data-stu-id="5a30d-163">Use the ORCFile format</span></span>
<span data-ttu-id="5a30d-164">Hive поддерживает различные форматы.</span><span class="sxs-lookup"><span data-stu-id="5a30d-164">Hive supports different file formats.</span></span> <span data-ttu-id="5a30d-165">Например:</span><span class="sxs-lookup"><span data-stu-id="5a30d-165">For example:</span></span>

* <span data-ttu-id="5a30d-166">**Текст**: это формат файла по умолчанию, работает с большинством сценариев</span><span class="sxs-lookup"><span data-stu-id="5a30d-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="5a30d-167">**Avro**: хорошо подходит для сценариев взаимодействия</span><span class="sxs-lookup"><span data-stu-id="5a30d-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="5a30d-168">**ORC/Parquet**: лучше всего подходит для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="5a30d-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="5a30d-169">Формат ORC (Optimized Row Columnar) — это очень эффективный способ хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="5a30d-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="5a30d-170">По сравнению с другими форматами ORC имеет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5a30d-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="5a30d-171">поддержка сложных типов, включая даты и время и частично структурированные и сложные типы</span><span class="sxs-lookup"><span data-stu-id="5a30d-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="5a30d-172">обеспечивает показатель сжатия данных до 70 %</span><span class="sxs-lookup"><span data-stu-id="5a30d-172">up to 70% compression</span></span>
* <span data-ttu-id="5a30d-173">индексирует каждые 10 000 строк, что позволяет пропускать строки;</span><span class="sxs-lookup"><span data-stu-id="5a30d-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="5a30d-174">обеспечивает существенное снижение времени выполнения запросов</span><span class="sxs-lookup"><span data-stu-id="5a30d-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="5a30d-175">Чтобы активировать ORC формат, необходимо сначала создать таблицу командой *Хранение в виде ORC*:</span><span class="sxs-lookup"><span data-stu-id="5a30d-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="5a30d-176">Далее необходимо выполнить вставку данных в таблицу ORC из промежуточной таблицы.</span><span class="sxs-lookup"><span data-stu-id="5a30d-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="5a30d-177">Например:</span><span class="sxs-lookup"><span data-stu-id="5a30d-177">For example:</span></span>

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

<span data-ttu-id="5a30d-178">Вы можете прочитать подробнее о формате ORC [здесь](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="5a30d-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="5a30d-179">Векторизация</span><span class="sxs-lookup"><span data-stu-id="5a30d-179">Vectorization</span></span>

<span data-ttu-id="5a30d-180">Векторизация позволяет Hive обрабатывать пакеты из 1024 строк одновременно вместо обработки каждой строки отдельно.</span><span class="sxs-lookup"><span data-stu-id="5a30d-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="5a30d-181">Это означает, что простые операции будут выполняться быстрее благодаря меньшему объему внутреннего кода, необходимого для запуска.</span><span class="sxs-lookup"><span data-stu-id="5a30d-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="5a30d-182">Чтобы активировать функцию векторизации, создайте запрос Hive со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="5a30d-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="5a30d-183">Для получения дополнительных сведений обратитесь к разделу [Выполнение векторизованного запроса](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="5a30d-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="5a30d-184">Другие методы оптимизации</span><span class="sxs-lookup"><span data-stu-id="5a30d-184">Other optimization methods</span></span>
<span data-ttu-id="5a30d-185">Существуют дополнительные методы оптимизации, которые также можно использовать, например:</span><span class="sxs-lookup"><span data-stu-id="5a30d-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="5a30d-186">**Группирование Hive** — техника, которая позволяет сегментировать или объединять в кластеры большие наборы данных для оптимизации производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="5a30d-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="5a30d-187">**Оптимизация объединений** — это оптимизация выполнения запросов Hive с целью повышения эффективности объединений и сокращения действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="5a30d-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="5a30d-188">Для получения дополнительных сведений обратитесь к разделу [Оптимизация объединений](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="5a30d-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="5a30d-189">**Увеличение модулей сжатия.**</span><span class="sxs-lookup"><span data-stu-id="5a30d-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a30d-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a30d-190">Next steps</span></span>
<span data-ttu-id="5a30d-191">В этой статье вы узнали некоторые распространенные методы оптимизации запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="5a30d-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="5a30d-192">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="5a30d-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="5a30d-193">Использование Apache Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a30d-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5a30d-194">Анализ данных о задержке рейсов с помощью Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a30d-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="5a30d-195">Анализ данных Twitter с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a30d-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="5a30d-196">Анализ данных датчика с помощью консоли запросов Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a30d-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="5a30d-197">Использование Hive в HDInsight для анализа журналов веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="5a30d-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
