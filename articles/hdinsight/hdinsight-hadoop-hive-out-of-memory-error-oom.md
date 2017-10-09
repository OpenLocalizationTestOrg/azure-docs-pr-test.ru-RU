---
title: "aaaFix Hive ошибка нехватки памяти в Azure HDInsight | Документы Microsoft"
description: "Устраните ошибку нехватки памяти Hive в HDInsight. сценарий Hello клиента — это запрос через много больших таблиц."
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
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="b29cf-105">Устранение ошибки нехватки памяти Hive в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b29cf-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="b29cf-106">Узнайте, как toofix Hive ошибка нехватки памяти при обработки больших таблиц, настроив параметры памяти Hive.</span><span class="sxs-lookup"><span data-stu-id="b29cf-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="b29cf-107">Выполнение запроса Hive к большим таблицам</span><span class="sxs-lookup"><span data-stu-id="b29cf-107">Run Hive query against large tables</span></span>

<span data-ttu-id="b29cf-108">Клиент выполнил запрос Hive.</span><span class="sxs-lookup"><span data-stu-id="b29cf-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="b29cf-109">Некоторые особенности этого запроса:</span><span class="sxs-lookup"><span data-stu-id="b29cf-109">Some nuances of this query:</span></span>

* <span data-ttu-id="b29cf-110">T1 является tooa большая таблица псевдонимов, Таблица1, в которой имеется несколько типов столбцов строки.</span><span class="sxs-lookup"><span data-stu-id="b29cf-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="b29cf-111">Другие таблицы не так велики, но имеют большое число столбцов.</span><span class="sxs-lookup"><span data-stu-id="b29cf-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="b29cf-112">Все таблицы соединяются друг с другом, в некоторых случаях с несколькими столбцами в TABLE1 и др.</span><span class="sxs-lookup"><span data-stu-id="b29cf-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="b29cf-113">запрос Hive Hello заняла 26 минут toofinish в кластере A3 HDInsight 24 узла.</span><span class="sxs-lookup"><span data-stu-id="b29cf-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="b29cf-114">Hello клиента, заметили-hello, следующие предупреждения:</span><span class="sxs-lookup"><span data-stu-id="b29cf-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="b29cf-115">С помощью подсистема выполнения Tez hello.</span><span class="sxs-lookup"><span data-stu-id="b29cf-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="b29cf-116">Hello того же запроса выполнялся в течение 15 минут, а затем вызвал hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="b29cf-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="b29cf-117">Ошибка Hello сохраняется при использовании больше виртуальной машины (например, D12).</span><span class="sxs-lookup"><span data-stu-id="b29cf-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="b29cf-118">Отладка hello ошибка нехватки памяти</span><span class="sxs-lookup"><span data-stu-id="b29cf-118">Debug hello out of memory error</span></span>

<span data-ttu-id="b29cf-119">Получение поддержки и инженеры вместе увидели, одна из проблем hello, вызывая hello ошибка нехватки памяти [известные проблемы, описанной в hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="b29cf-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="b29cf-120">Hello **hive.auto.convert.join.noconditionaltask** в hello hive-site.xml файла было задано слишком**true**:</span><span class="sxs-lookup"><span data-stu-id="b29cf-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="b29cf-121">Вполне вероятно, карты соединения была hello причину hello пространства кучи Java нашей недостатке памяти.</span><span class="sxs-lookup"><span data-stu-id="b29cf-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="b29cf-122">Как описано в записи блога hello [параметры памяти Hadoop Yarn в HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), когда подсистема выполнения является занятое кучи используется hello Tez фактически относится toohello Tez контейнера.</span><span class="sxs-lookup"><span data-stu-id="b29cf-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="b29cf-123">См. следующие изображения описания hello Tez контейнера памяти hello.</span><span class="sxs-lookup"><span data-stu-id="b29cf-123">See hello following image describing hello Tez container memory.</span></span>

![Схема памяти контейнера Tez: ошибка нехватки памяти Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="b29cf-125">Как видно в блоге hello, hello, следующие два параметра памяти определить hello контейнера памяти для кучи hello: **hive.tez.container.size** и **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="b29cf-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="b29cf-126">Наш опыта hello исключения, находящегося вне не означает, что размер контейнера hello слишком мал.</span><span class="sxs-lookup"><span data-stu-id="b29cf-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="b29cf-127">Это означает, что размер кучи Java (hive.tez.java.opts) hello слишком мал.</span><span class="sxs-lookup"><span data-stu-id="b29cf-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="b29cf-128">Поэтому каждый раз, когда вы видите не хватает памяти, можно попробовать tooincrease **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="b29cf-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="b29cf-129">При необходимости может потребоваться tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="b29cf-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="b29cf-130">Hello **java.opts** значение параметра должно быть приблизительно 80% от **container.size**.</span><span class="sxs-lookup"><span data-stu-id="b29cf-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="b29cf-131">параметр Hello **hive.tez.java.opts** всегда должен быть меньше, чем **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="b29cf-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="b29cf-132">Так как машине D12 28 ГБ памяти, мы решили toouse размер контейнера 10 ГБ (10240 МБ) и назначить toojava.opts 80%:</span><span class="sxs-lookup"><span data-stu-id="b29cf-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="b29cf-133">С новыми настройками hello hello успешно выполнен запрос в разделе через 10 минут.</span><span class="sxs-lookup"><span data-stu-id="b29cf-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b29cf-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b29cf-134">Next steps</span></span>

<span data-ttu-id="b29cf-135">Сообщение об ошибке нехватки памяти не обязательно означает, что размер контейнера hello слишком мал.</span><span class="sxs-lookup"><span data-stu-id="b29cf-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="b29cf-136">Вместо этого вы должны настроить параметры памяти hello, увеличивается размер кучи hello, а затем — по крайней мере 80% от размера памяти контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="b29cf-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="b29cf-137">Дополнительные сведения см. в статье [Оптимизация запросов Hive для Hadoop в HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="b29cf-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
