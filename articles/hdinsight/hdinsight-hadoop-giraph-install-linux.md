---
title: "aaaInstall и использовать Giraph на HDInsight (Hadoop) - Azure | Документы Microsoft"
description: "Узнайте, как tooinstall Giraph на основе Linux HDInsight кластеры, использующие действий скрипта. Действия сценариев позволяют toocustomize hello кластера во время создания, путем изменения конфигурации кластера или установка служб и программ."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="3e7cf-104">Установка Giraph в кластерах HDInsight Hadoop и крупномасштабных графы tooprocess Giraph</span><span class="sxs-lookup"><span data-stu-id="3e7cf-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="3e7cf-105">Узнайте, как tooinstall Apache Giraph в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="3e7cf-106">Hello скрипт действие hdinsight, позволяет toocustomize кластера, запустив сценарий bash.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="3e7cf-107">Сценарии могут быть кластеров используется toocustomize во время и после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e7cf-108">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3e7cf-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3e7cf-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3e7cf-111"><a name="whatis"></a>Что такое Giraph</span><span class="sxs-lookup"><span data-stu-id="3e7cf-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="3e7cf-112">[Apache Giraph](http://giraph.apache.org/) дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="3e7cf-113">Графы моделируют взаимоотношения между объектами.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="3e7cf-114">Например hello подключений между маршрутизаторами в больших сетях, например hello Интернет или связи между пользователями в социальных сетях.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="3e7cf-115">Обработка Graph позволяет tooreason о hello связей между объектами в граф, такие как:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="3e7cf-116">определение потенциальных друзей на основе текущих взаимоотношений;</span><span class="sxs-lookup"><span data-stu-id="3e7cf-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="3e7cf-117">Определение hello кратчайший маршрут между двумя компьютерами в сети.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="3e7cf-118">Вычисление ранга hello страницы веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="3e7cf-119">Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются - службу технической поддержки Майкрософт помогает tooisolate и разрешить проблемы toothese связанные компоненты.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="3e7cf-120">Пользовательские компоненты, такие как Giraph, получать toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="3e7cf-121">Службу технической поддержки Майкрософт может быть проблема может tooresolving hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="3e7cf-122">В противном случае необходимо обратиться в сообщество разработчиков открытого кода, обладающих большим опытом в этой сфере.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="3e7cf-123">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="3e7cf-124">Какие hello скрипта</span><span class="sxs-lookup"><span data-stu-id="3e7cf-124">What hello script does</span></span>

<span data-ttu-id="3e7cf-125">Скрипт выполняет следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="3e7cf-126">Устанавливает Giraph слишком`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="3e7cf-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="3e7cf-127">Копирует hello `giraph-examples.jar` toodefault хранилище файлов (WASB) для кластера:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="3e7cf-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="3e7cf-128"><a name="install"></a>Установка Giraph с помощью действий сценария</span><span class="sxs-lookup"><span data-stu-id="3e7cf-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="3e7cf-129">Пример сценария tooinstall Giraph в кластере HDInsight доступна на hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="3e7cf-130">В этом разделе описано, как toouse hello образец скрипта при создании hello кластера с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3e7cf-131">Действие сценария можно применить, используя любой из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="3e7cf-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e7cf-132">Azure PowerShell</span></span>
> * <span data-ttu-id="3e7cf-133">Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3e7cf-133">hello Azure CLI</span></span>
> * <span data-ttu-id="3e7cf-134">Hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3e7cf-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="3e7cf-135">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="3e7cf-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="3e7cf-136">Можно также применить tooalready действия сценария работающие кластеры.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="3e7cf-137">Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="3e7cf-138">Начать создание кластера с помощью действия hello в [кластеры HDInsight под управлением Linux, создать](hdinsight-hadoop-create-linux-clusters-portal.md), но не завершайте создания.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="3e7cf-139">На hello **необязательная конфигурация** колонке выберите **действия скрипта**и укажите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="3e7cf-140">**ИМЯ**: Введите понятное имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="3e7cf-141">**URI СКРИПТА**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="3e7cf-142">**Головной**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="3e7cf-143">**Рабочий**: не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3e7cf-144">**ZOOKEEPER**: не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3e7cf-145">**ПАРАМЕТРЫ**: оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="3e7cf-146">Внизу hello hello **действия скрипта**, использовать hello **выберите** конфигурация hello toosave кнопок.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="3e7cf-147">Наконец, используйте hello **выберите** кнопку внизу hello hello **необязательная конфигурация** колонке toosave hello необязательная конфигурация сведения.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="3e7cf-148">Продолжить создание кластера hello, как описано в [кластеры HDInsight под управлением Linux, создать](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="3e7cf-149"><a name="usegiraph"></a>Как использовать Giraph в HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e7cf-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="3e7cf-150">После создания hello кластера с помощью hello, входящий в состав Giraph SimpleShortestPathsComputation пример действия toorun hello ниже.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="3e7cf-151">В этом примере используется hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) реализацию для обнаружения hello кратчайшего пути между объектами в граф.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="3e7cf-152">Подключите кластер HDInsight toohello с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3e7cf-153">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3e7cf-154">Используйте hello следующая команда toocreate файл с именем **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="3e7cf-155">Используйте hello после текста как hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="3e7cf-156">Эти данные описывает связь между объектами в направленный граф, используя формат hello `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="3e7cf-157">Каждая строка представляет взаимоотношение между объектом `source_id` и одним или несколькими объектами `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="3e7cf-158">Hello `edge_value` можно рассматривать как стойкость hello или расстояние hello соединения между `source_id` и `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="3e7cf-159">Рисования, используя значение hello (или вес) в качестве hello расстояния между объектами, hello данных может выглядеть, как hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt начерчен в виде кругов с линиями различной длины между](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="3e7cf-161">toosave hello файла, используйте **Ctrl + X**, затем **Y**и, наконец, **ввод** имя файла tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="3e7cf-162">Используйте следующие данные toostore hello в основного хранилища для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="3e7cf-163">Выполнение примера SimpleShortestPathsComputation hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="3e7cf-164">в hello в следующей таблице описаны Hello параметров, используемых с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="3e7cf-165">Параметр</span><span class="sxs-lookup"><span data-stu-id="3e7cf-165">Parameter</span></span> | <span data-ttu-id="3e7cf-166">Действие</span><span class="sxs-lookup"><span data-stu-id="3e7cf-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="3e7cf-167">Hello jar файл, содержащий примеры hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="3e7cf-168">Класс Hello использовать примеры toostart hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="3e7cf-169">пример Hello, используется.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-169">hello example that is used.</span></span> <span data-ttu-id="3e7cf-170">В этом примере вычисляется hello кратчайшего пути между Идентификатором 1 и все идентификаторы в hello graph.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="3e7cf-171">Hello головному узлу кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="3e7cf-172">Hello toouse входной формат для hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="3e7cf-173">файл входных данных Hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="3e7cf-174">Формат вывода Hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-174">hello output format.</span></span> <span data-ttu-id="3e7cf-175">В данном примере — ИД и значение в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="3e7cf-176">выходное расположение Hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="3e7cf-177">Количество работников toouse Hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-177">hello number of workers toouse.</span></span> <span data-ttu-id="3e7cf-178">В этом примере — 2.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-178">In this example, 2.</span></span> |

    <span data-ttu-id="3e7cf-179">Дополнительные сведения об этих и других параметров, используемых с образцами Giraph см. в разделе hello [краткое руководство Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="3e7cf-180">По завершении задания hello hello результаты сохраняются в hello **/example/out/shotestpaths** каталога.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="3e7cf-181">Hello имена выходных файлов начинаются с **часть-m -** и заканчиваться число, указывающее hello во-первых, во-вторых, т. д. файл.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="3e7cf-182">Используйте следующие выходные данные команды tooview hello hello.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="3e7cf-183">Hello вывод должен выглядеть примерно toohello после текста:</span><span class="sxs-lookup"><span data-stu-id="3e7cf-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="3e7cf-184">Пример SimpleShortestPathComputation Hello является жестко заданный toostart с Идентификатором 1 объекта и поиска hello кратчайший путь tooother объектов.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="3e7cf-185">Hello выводится в формате hello `destination_id` и `distance`.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="3e7cf-186">Hello `distance` равно hello значение (вес) границ hello пути между объектом с Идентификатором 1 и идентификатором hello объекта.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="3e7cf-187">Визуализации, можно проверить результаты hello, проходящих hello кратчайшего пути между Идентификатором 1 и других объектов.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="3e7cf-188">Hello кратчайшего пути между 1 идентификатор и идентификатор 4 — 5.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="3e7cf-189">Это значение является hello общее расстояние между <span style="color:orange">идентификатор 1 и 3</span>, а затем <span style="color:red">идентификатор 3 и 4</span>.</span><span class="sxs-lookup"><span data-stu-id="3e7cf-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Представление объектов в виде кругов с кратчайшими путями между ними](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="3e7cf-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e7cf-191">Next steps</span></span>

* <span data-ttu-id="3e7cf-192">[Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="3e7cf-193">[Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e7cf-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
