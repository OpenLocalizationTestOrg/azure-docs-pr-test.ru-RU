---
title: "aaaTroubleshoot Hive с помощью Azure HDInsight | Документы Microsoft"
description: "Ответы toocommon вопросов о работе с Apache Hive и Azure HDInsight."
keywords: "Azure HDInsight, Hive, вопросы и ответы, руководство по устранению неполадок, часто задаваемые вопросы"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="dd61f-104">Устранение неполадок в Hive с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd61f-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="dd61f-105">Дополнительные сведения о наиболее важные вопросы hello и способы их устранения при работе с Apache Hive полезных данных в Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="dd61f-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="dd61f-106">Как экспортировать хранилище метаданных Hive и импортировать его в другой кластер?</span><span class="sxs-lookup"><span data-stu-id="dd61f-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="dd61f-107">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="dd61f-107">Resolution steps</span></span>

1. <span data-ttu-id="dd61f-108">Подключите кластер HDInsight toohello с помощью клиента Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="dd61f-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="dd61f-109">Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="dd61f-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="dd61f-110">Выполните следующую команду в кластере HDInsight hello, из которого нужно метахранилище hello tooexport hello.</span><span class="sxs-lookup"><span data-stu-id="dd61f-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="dd61f-111">Эта команда создает файл с именем allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="dd61f-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="dd61f-112">Скопируйте hello файл alltables.sql toohello новый кластер HDInsight, а затем запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dd61f-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="dd61f-113">Hello кода hello устранению предполагает, что данные, которые являются пути на новый кластер hello hello таким же как пути к данным hello hello старом кластере.</span><span class="sxs-lookup"><span data-stu-id="dd61f-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="dd61f-114">Если отличаются пути к данным hello, можно вручную отредактировать созданные hello alltables.sql файл tooreflect любые изменения.</span><span class="sxs-lookup"><span data-stu-id="dd61f-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="dd61f-115">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="dd61f-115">Additional reading</span></span>

- [<span data-ttu-id="dd61f-116">Подключите кластер HDInsight tooan с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="dd61f-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="dd61f-117">Как найти журналы Hive в кластере?</span><span class="sxs-lookup"><span data-stu-id="dd61f-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="dd61f-118">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="dd61f-118">Resolution steps</span></span>

1. <span data-ttu-id="dd61f-119">Подключите кластер HDInsight toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="dd61f-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="dd61f-120">Подробные сведения см. в разделе **Дополнительные материалы**.</span><span class="sxs-lookup"><span data-stu-id="dd61f-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="dd61f-121">журналы клиента куст tooview, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dd61f-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="dd61f-122">журналы метахранилища Hive tooview, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dd61f-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="dd61f-123">журналы Hiveserver tooview, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dd61f-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="dd61f-124">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="dd61f-124">Additional reading</span></span>

- [<span data-ttu-id="dd61f-125">Подключите кластер HDInsight tooan с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="dd61f-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="dd61f-126">Как запустить hello оболочки Hive с определенных конфигураций в кластере</span><span class="sxs-lookup"><span data-stu-id="dd61f-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="dd61f-127">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="dd61f-127">Resolution steps</span></span>

1. <span data-ttu-id="dd61f-128">Укажите пару ключ значение конфигурации при запуске hello Hive оболочки.</span><span class="sxs-lookup"><span data-stu-id="dd61f-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="dd61f-129">Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="dd61f-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="dd61f-130">toolist все действующие конфигурации Hive оболочки, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="dd61f-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="dd61f-131">Например можно используйте следующие командной оболочки куст toostart журнала отладки на консоль hello hello:</span><span class="sxs-lookup"><span data-stu-id="dd61f-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="dd61f-132">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="dd61f-132">Additional reading</span></span>

- [<span data-ttu-id="dd61f-133">Свойства конфигурации Hive</span><span class="sxs-lookup"><span data-stu-id="dd61f-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="dd61f-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Как анализировать данные направленного ациклического графа Tez по критическому пути кластера?</span><span class="sxs-lookup"><span data-stu-id="dd61f-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="dd61f-135">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="dd61f-135">Resolution steps</span></span>
 
1. <span data-ttu-id="dd61f-136">подключение toohello кластера HDInsight с помощью SSH, tooanalyze Tez Apache направленный ациклического графа (DAG) на диаграмме кластеров с точки зрения безопасности.</span><span class="sxs-lookup"><span data-stu-id="dd61f-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="dd61f-137">Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="dd61f-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="dd61f-138">В командной строке выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="dd61f-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="dd61f-139">toolist других анализаторы, которые можно использовать tooanalyze Tez DAG использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dd61f-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="dd61f-140">Пример программы необходимо указать в качестве первого аргумента hello.</span><span class="sxs-lookup"><span data-stu-id="dd61f-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="dd61f-141">Допустимые имена программы:</span><span class="sxs-lookup"><span data-stu-id="dd61f-141">Valid program names include:</span></span>
    - <span data-ttu-id="dd61f-142">**ContainerReuseAnalyzer** — печать сведений о повторном использовании контейнера в DAG;</span><span class="sxs-lookup"><span data-stu-id="dd61f-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="dd61f-143">**CriticalPath**: критический путь поиска hello в DAG</span><span class="sxs-lookup"><span data-stu-id="dd61f-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="dd61f-144">**LocalityAnalyzer** — печать сведений о местоположении в DAG;</span><span class="sxs-lookup"><span data-stu-id="dd61f-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="dd61f-145">**ShuffleTimeAnalyzer**: анализ подробностями времени смещения hello в группе DAG</span><span class="sxs-lookup"><span data-stu-id="dd61f-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="dd61f-146">**SkewAnalyzer**: анализ hello наклона сведений в группе DAG</span><span class="sxs-lookup"><span data-stu-id="dd61f-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="dd61f-147">**SlowNodeAnalyzer** — печать сведений об узле в DAG;</span><span class="sxs-lookup"><span data-stu-id="dd61f-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="dd61f-148">**SlowTaskIdentifier** — печать сведений о медленных задачах в DAG;</span><span class="sxs-lookup"><span data-stu-id="dd61f-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="dd61f-149">**SlowestVertexAnalyzer** — печать сведений о медленных вершинах в DAG;</span><span class="sxs-lookup"><span data-stu-id="dd61f-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="dd61f-150">**SpillAnalyzer** — печать сведений о перемещении в DAG;</span><span class="sxs-lookup"><span data-stu-id="dd61f-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="dd61f-151">**TaskConcurrencyAnalyzer**: печать параллелизма сведения о задаче hello в группе DAG</span><span class="sxs-lookup"><span data-stu-id="dd61f-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="dd61f-152">**VertexLevelCriticalPathAnalyzer**: hello критическим поиска на уровне вершин в группе DAG</span><span class="sxs-lookup"><span data-stu-id="dd61f-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="dd61f-153">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="dd61f-153">Additional reading</span></span>

- [<span data-ttu-id="dd61f-154">Подключите кластер HDInsight tooan с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="dd61f-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="dd61f-155">Как скачать данные направленного ациклического графа Tez из кластера?</span><span class="sxs-lookup"><span data-stu-id="dd61f-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="dd61f-156">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="dd61f-156">Resolution steps</span></span>

<span data-ttu-id="dd61f-157">Существует два способа toocollect hello Tez DAG данных:</span><span class="sxs-lookup"><span data-stu-id="dd61f-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="dd61f-158">Из командной строки hello:</span><span class="sxs-lookup"><span data-stu-id="dd61f-158">From hello command line:</span></span>
 
    <span data-ttu-id="dd61f-159">Подключите кластер HDInsight toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="dd61f-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="dd61f-160">Hello командной строки выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="dd61f-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="dd61f-161">Используйте представление Ambari Tez hello.</span><span class="sxs-lookup"><span data-stu-id="dd61f-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="dd61f-162">Go tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="dd61f-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="dd61f-163">Последовательно выберите tooTez представление (под значком плитки hello в правом верхнем углу hello).</span><span class="sxs-lookup"><span data-stu-id="dd61f-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="dd61f-164">Выберите hello требуется tooview DAG.</span><span class="sxs-lookup"><span data-stu-id="dd61f-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="dd61f-165">Выберите **Скачать данные**.</span><span class="sxs-lookup"><span data-stu-id="dd61f-165">Select **Download data**.</span></span>

### <span data-ttu-id="dd61f-166"><a name="additional-reading-end"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="dd61f-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="dd61f-167">Подключите кластер HDInsight tooan с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="dd61f-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






