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
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Устранение ошибки нехватки памяти Hive в Azure HDInsight

Узнайте, как toofix Hive ошибка нехватки памяти при обработки больших таблиц, настроив параметры памяти Hive.

## <a name="run-hive-query-against-large-tables"></a>Выполнение запроса Hive к большим таблицам

Клиент выполнил запрос Hive.

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

Некоторые особенности этого запроса:

* T1 является tooa большая таблица псевдонимов, Таблица1, в которой имеется несколько типов столбцов строки.
* Другие таблицы не так велики, но имеют большое число столбцов.
* Все таблицы соединяются друг с другом, в некоторых случаях с несколькими столбцами в TABLE1 и др.

запрос Hive Hello заняла 26 минут toofinish в кластере A3 HDInsight 24 узла. Hello клиента, заметили-hello, следующие предупреждения:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

С помощью подсистема выполнения Tez hello. Hello того же запроса выполнялся в течение 15 минут, а затем вызвал hello следующая ошибка:

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

Ошибка Hello сохраняется при использовании больше виртуальной машины (например, D12).


## <a name="debug-hello-out-of-memory-error"></a>Отладка hello ошибка нехватки памяти

Получение поддержки и инженеры вместе увидели, одна из проблем hello, вызывая hello ошибка нехватки памяти [известные проблемы, описанной в hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

Hello **hive.auto.convert.join.noconditionaltask** в hello hive-site.xml файла было задано слишком**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

Вполне вероятно, карты соединения была hello причину hello пространства кучи Java нашей недостатке памяти. Как описано в записи блога hello [параметры памяти Hadoop Yarn в HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), когда подсистема выполнения является занятое кучи используется hello Tez фактически относится toohello Tez контейнера. См. следующие изображения описания hello Tez контейнера памяти hello.

![Схема памяти контейнера Tez: ошибка нехватки памяти Hive](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

Как видно в блоге hello, hello, следующие два параметра памяти определить hello контейнера памяти для кучи hello: **hive.tez.container.size** и **hive.tez.java.opts**. Наш опыта hello исключения, находящегося вне не означает, что размер контейнера hello слишком мал. Это означает, что размер кучи Java (hive.tez.java.opts) hello слишком мал. Поэтому каждый раз, когда вы видите не хватает памяти, можно попробовать tooincrease **hive.tez.java.opts**. При необходимости может потребоваться tooincrease **hive.tez.container.size**. Hello **java.opts** значение параметра должно быть приблизительно 80% от **container.size**.

> [!NOTE]
> параметр Hello **hive.tez.java.opts** всегда должен быть меньше, чем **hive.tez.container.size**.
> 
> 

Так как машине D12 28 ГБ памяти, мы решили toouse размер контейнера 10 ГБ (10240 МБ) и назначить toojava.opts 80%:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

С новыми настройками hello hello успешно выполнен запрос в разделе через 10 минут.

## <a name="next-steps"></a>Дальнейшие действия

Сообщение об ошибке нехватки памяти не обязательно означает, что размер контейнера hello слишком мал. Вместо этого вы должны настроить параметры памяти hello, увеличивается размер кучи hello, а затем — по крайней мере 80% от размера памяти контейнер hello. Дополнительные сведения см. в статье [Оптимизация запросов Hive для Hadoop в HDInsight](hdinsight-hadoop-optimize-hive-query.md).
