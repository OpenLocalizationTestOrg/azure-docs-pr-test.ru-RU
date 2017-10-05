---
title: "Устранение ошибки нехватки памяти Hive в Azure HDInsight | Документы Майкрософт"
description: "Устраните ошибку нехватки памяти Hive в HDInsight. Пользовательский сценарий представляет собой запрос ко множеству больших таблиц."
keywords: "ошибка нехватки памяти, OOM, параметры Hive"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: da1247070ade11f78b505524f5e970e18eb16d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="058a9-105">Устранение ошибки нехватки памяти Hive в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="058a9-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="058a9-106">Узнайте, как устранить ошибку нехватки памяти Hive при обработке больших таблиц в настройках памяти Hive.</span><span class="sxs-lookup"><span data-stu-id="058a9-106">Learn how to fix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="058a9-107">Выполнение запроса Hive к большим таблицам</span><span class="sxs-lookup"><span data-stu-id="058a9-107">Run Hive query against large tables</span></span>

<span data-ttu-id="058a9-108">Клиент выполнил запрос Hive.</span><span class="sxs-lookup"><span data-stu-id="058a9-108">A customer ran a Hive query:</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="058a9-109">Некоторые особенности этого запроса:</span><span class="sxs-lookup"><span data-stu-id="058a9-109">Some nuances of this query:</span></span>

* <span data-ttu-id="058a9-110">T1 является псевдонимом для большой таблицы TABLE1, которая содержит множество столбцов типа STRING.</span><span class="sxs-lookup"><span data-stu-id="058a9-110">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="058a9-111">Другие таблицы не так велики, но имеют большое число столбцов.</span><span class="sxs-lookup"><span data-stu-id="058a9-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="058a9-112">Все таблицы соединяются друг с другом, в некоторых случаях с несколькими столбцами в TABLE1 и др.</span><span class="sxs-lookup"><span data-stu-id="058a9-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="058a9-113">На выполнение запроса Hive в кластере HDInsight A3 с 24 узлами ушло 26 минут.</span><span class="sxs-lookup"><span data-stu-id="058a9-113">The Hive query took 26 minutes to finish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="058a9-114">Клиент заметил следующие предупреждения:</span><span class="sxs-lookup"><span data-stu-id="058a9-114">The customer noticed the following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="058a9-115">С механизмом выполнения Tez</span><span class="sxs-lookup"><span data-stu-id="058a9-115">By using the Tez execution engine.</span></span> <span data-ttu-id="058a9-116">выполнение того же запроса заняло 15 минут, после чего появилась следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="058a9-116">The same query ran for 15 minutes, and then threw the following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="058a9-117">Ошибка не устраняется при использовании виртуальной машины большего размера (например, D12).</span><span class="sxs-lookup"><span data-stu-id="058a9-117">The error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-the-out-of-memory-error"></a><span data-ttu-id="058a9-118">Отладка ошибки нехватки памяти</span><span class="sxs-lookup"><span data-stu-id="058a9-118">Debug the out of memory error</span></span>

<span data-ttu-id="058a9-119">Наша инженерная команда и команда поддержки обнаружили, что одна из проблем, которые приводят к ошибке нехватки памяти, представляет собой [известную проблему, описанную в Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306).</span><span class="sxs-lookup"><span data-stu-id="058a9-119">Our support and engineering teams together found one of the issues causing the out of memory error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="058a9-120">Для свойства **hive.auto.convert.join.noconditionaltask** в файле hive-site.xml задано значение **true**:</span><span class="sxs-lookup"><span data-stu-id="058a9-120">The **hive.auto.convert.join.noconditionaltask** in the hive-site.xml file was set to **true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="058a9-121">Вполне вероятно, что источником ошибки нехватки памяти в пространстве кучи Java был Map Join.</span><span class="sxs-lookup"><span data-stu-id="058a9-121">It is likely map join was the cause of the Java Heap Space our of memory error.</span></span> <span data-ttu-id="058a9-122">Как описано в записи блога [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx) (Параметры памяти Hadoop Yarn в HDInsight), при использовании модуля Tez используемое пространство кучи на самом деле принадлежит контейнеру Tez.</span><span class="sxs-lookup"><span data-stu-id="058a9-122">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="058a9-123">Описание памяти контейнера Tez см. на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="058a9-123">See the following image describing the Tez container memory.</span></span>

![Схема памяти контейнера Tez: ошибка нехватки памяти Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="058a9-125">Как следует из записи блога, два следующих параметра памяти определяют контейнер памяти для кучи: **hive.tez.container.size** и **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="058a9-125">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="058a9-126">Согласно нашему опыту, исключение нехватки памяти не означает, что размер контейнера слишком мал.</span><span class="sxs-lookup"><span data-stu-id="058a9-126">From our experience, the out of memory exception does not mean the container size is too small.</span></span> <span data-ttu-id="058a9-127">Оно означает, что размер кучи Java (hive.tez.java.opts) слишком мал.</span><span class="sxs-lookup"><span data-stu-id="058a9-127">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="058a9-128">Поэтому каждый раз, когда вы видите ошибку нехватки памяти, можно попытаться увеличить **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="058a9-128">So whenever you see out of memory, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="058a9-129">При необходимости может потребоваться увеличение параметра **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="058a9-129">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="058a9-130">Параметр **Java.opts** должен составлять около 80 % от **container.size**.</span><span class="sxs-lookup"><span data-stu-id="058a9-130">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="058a9-131">Параметр **hive.tez.java.opts** всегда должен быть меньше, чем **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="058a9-131">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="058a9-132">Так как виртуальная машина размера D12 имеет 28 ГБ памяти, мы решили использовать контейнер размером 10 ГБ (10 240 МБ) и назначить 80 % от этого размера параметру java.opts.</span><span class="sxs-lookup"><span data-stu-id="058a9-132">Because a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="058a9-133">С новыми настройками запрос был выполнен успешно за 10 минут.</span><span class="sxs-lookup"><span data-stu-id="058a9-133">With the new settings, the query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="058a9-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="058a9-134">Next steps</span></span>

<span data-ttu-id="058a9-135">Ошибка нехватки памяти не обязательно означает, что размер контейнера слишком мал.</span><span class="sxs-lookup"><span data-stu-id="058a9-135">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="058a9-136">Вместо этого следует настроить параметры памяти, увеличив размер кучи, так чтобы он составлял не менее 80 % от размера памяти контейнера.</span><span class="sxs-lookup"><span data-stu-id="058a9-136">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span> <span data-ttu-id="058a9-137">Дополнительные сведения см. в статье [Оптимизация запросов Hive для Hadoop в HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="058a9-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>