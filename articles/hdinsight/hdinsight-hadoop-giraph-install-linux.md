---
title: "Установка и использование Giraph в кластерах HDInsight (Hadoop) — Azure | Документы Майкрософт"
description: "Узнайте, как устанавливать Giraph в кластерах HDInsight на основе Linux с помощью действий сценария. Действия сценария позволяют настроить кластер во время создания, изменяя его конфигурацию или устанавливая службы и служебные программы."
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
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="5f094-104">Установка Giraph в кластерах HDInsight Hadoop и использование Giraph для обработки диаграмм больших объемов</span><span class="sxs-lookup"><span data-stu-id="5f094-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="5f094-105">Узнайте, как установить Apache Giraph в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f094-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="5f094-106">Действие сценария в HDInsight позволяет настроить кластер с помощью сценария bash.</span><span class="sxs-lookup"><span data-stu-id="5f094-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="5f094-107">Сценарии можно использовать для настройки кластеров во время и после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="5f094-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f094-108">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="5f094-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5f094-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="5f094-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5f094-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5f094-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="5f094-111"><a name="whatis"></a>Что такое Giraph</span><span class="sxs-lookup"><span data-stu-id="5f094-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="5f094-112">[Apache Giraph](http://giraph.apache.org/) позволяет обрабатывать графы с помощью Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f094-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="5f094-113">Графы моделируют взаимоотношения между объектами.</span><span class="sxs-lookup"><span data-stu-id="5f094-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="5f094-114">Например, подключения между маршрутизаторами в большой сети, подобной Интернету, или взаимоотношения между людьми в социальных сетях.</span><span class="sxs-lookup"><span data-stu-id="5f094-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="5f094-115">Обработка графов дает возможность делать выводы о взаимоотношениях объектов в графе, таких как:</span><span class="sxs-lookup"><span data-stu-id="5f094-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="5f094-116">определение потенциальных друзей на основе текущих взаимоотношений;</span><span class="sxs-lookup"><span data-stu-id="5f094-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="5f094-117">определение кратчайшего маршрута между двумя компьютерами в сети;</span><span class="sxs-lookup"><span data-stu-id="5f094-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="5f094-118">вычисление ранга страницы для веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="5f094-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="5f094-119">Компоненты, предоставляемые вместе с кластером HDInsight, поддерживаются в полном объеме. Служба технической поддержки Майкрософт помогает выявить и решить проблемы, связанные с этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="5f094-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="5f094-120">Настраиваемые компоненты, такие как Giraph, получают ограниченную коммерчески оправданную поддержку, способствующую дальнейшей диагностике проблемы.</span><span class="sxs-lookup"><span data-stu-id="5f094-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="5f094-121">Эту проблему может решить служба технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5f094-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="5f094-122">В противном случае необходимо обратиться в сообщество разработчиков открытого кода, обладающих большим опытом в этой сфере.</span><span class="sxs-lookup"><span data-stu-id="5f094-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="5f094-123">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="5f094-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="5f094-124">Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).</span><span class="sxs-lookup"><span data-stu-id="5f094-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="5f094-125">Что делает сценарий</span><span class="sxs-lookup"><span data-stu-id="5f094-125">What the script does</span></span>

<span data-ttu-id="5f094-126">Сценарий выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5f094-126">This script performs the following actions:</span></span>

* <span data-ttu-id="5f094-127">Устанавливает Giraph в `/usr/hdp/current/giraph`.</span><span class="sxs-lookup"><span data-stu-id="5f094-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="5f094-128">Копирует файл `giraph-examples.jar` в хранилище по умолчанию (WASB) в кластере: `/example/jars/giraph-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="5f094-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="5f094-129"><a name="install"></a>Установка Giraph с помощью действий сценария</span><span class="sxs-lookup"><span data-stu-id="5f094-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="5f094-130">Пример сценария для установки Giraph в кластер HDInsight доступен по следующему адресу:</span><span class="sxs-lookup"><span data-stu-id="5f094-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="5f094-131">Этот раздел содержит инструкции по использованию примера сценария при создании кластера с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5f094-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5f094-132">Действие сценария может применяться следующими способами:</span><span class="sxs-lookup"><span data-stu-id="5f094-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="5f094-133">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f094-133">Azure PowerShell</span></span>
> * <span data-ttu-id="5f094-134">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5f094-134">The Azure CLI</span></span>
> * <span data-ttu-id="5f094-135">Пакет SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="5f094-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="5f094-136">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="5f094-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="5f094-137">Действия сценария также можно применять к уже работающим кластерам.</span><span class="sxs-lookup"><span data-stu-id="5f094-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="5f094-138">Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5f094-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="5f094-139">Приступите к созданию кластера с помощью действий, описанных в разделе [Создание кластеров HDInsight под управлением Linux](hdinsight-hadoop-create-linux-clusters-portal.md), но не завершайте создание.</span><span class="sxs-lookup"><span data-stu-id="5f094-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="5f094-140">В колонке **Необязательная настройка** выберите **Действия сценария** и введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="5f094-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="5f094-141">**ИМЯ**: введите понятное имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="5f094-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="5f094-142">**URI СКРИПТА**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh.</span><span class="sxs-lookup"><span data-stu-id="5f094-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="5f094-143">**Головной**: установите флажок.</span><span class="sxs-lookup"><span data-stu-id="5f094-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="5f094-144">**Рабочий**: не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="5f094-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="5f094-145">**ZOOKEEPER**: не устанавливайте этот флажок.</span><span class="sxs-lookup"><span data-stu-id="5f094-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="5f094-146">**ПАРАМЕТРЫ**: оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="5f094-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="5f094-147">В нижней части раздела **Действия скрипта** нажмите кнопку **Выбрать**, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="5f094-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="5f094-148">Наконец, в нижней части колонки **Дополнительная конфигурация** нажмите кнопку **Выбрать**, чтобы сохранить дополнительные настройки.</span><span class="sxs-lookup"><span data-stu-id="5f094-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="5f094-149">Продолжите создание кластера, как описано в разделе [Создание кластеров HDInsight под управлением Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5f094-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="5f094-150"><a name="usegiraph"></a>Как использовать Giraph в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f094-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="5f094-151">После создания кластера выполните следующие действия, чтобы запустить пример SimpleShortestPathsComputation (входит в Giraph).</span><span class="sxs-lookup"><span data-stu-id="5f094-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="5f094-152">В примере использована простая реализация [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) для поиска кратчайшего пути между объектами в графе.</span><span class="sxs-lookup"><span data-stu-id="5f094-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="5f094-153">Подключитесь к кластеру HDInsight с помощью протокола SSH:</span><span class="sxs-lookup"><span data-stu-id="5f094-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="5f094-154">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5f094-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5f094-155">Создайте файл **tiny_graph.txt**, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5f094-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="5f094-156">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="5f094-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="5f094-157">Эти данные описывают взаимоотношения между объектами в направленном графе с использованием формата `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="5f094-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="5f094-158">Каждая строка представляет взаимоотношение между объектом `source_id` и одним или несколькими объектами `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="5f094-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="5f094-159">Значение `edge_value` можно представить себе как силу или расстояние подключения между `source_id` и `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="5f094-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="5f094-160">В визуальной форме и с использованием значения (или веса) в качестве расстояния между объектами данные могут выглядеть, как показано на следующей схеме.</span><span class="sxs-lookup"><span data-stu-id="5f094-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![tiny_graph.txt начерчен в виде кругов с линиями различной длины между](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="5f094-162">Чтобы сохранить файл, нажмите **CTRL+X**, затем **Y** и **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="5f094-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="5f094-163">Чтобы сохранить данные в основном хранилище в кластере HDInsight, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f094-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="5f094-164">Запустите пример SimpleShortestPathsComputation, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f094-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="5f094-165">В следующей таблице описаны параметры, используемые в этой команде.</span><span class="sxs-lookup"><span data-stu-id="5f094-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="5f094-166">Параметр</span><span class="sxs-lookup"><span data-stu-id="5f094-166">Parameter</span></span> | <span data-ttu-id="5f094-167">Действие</span><span class="sxs-lookup"><span data-stu-id="5f094-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="5f094-168">JAR-файл, содержащий примеры.</span><span class="sxs-lookup"><span data-stu-id="5f094-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="5f094-169">Класс, используемый для запуска примеров.</span><span class="sxs-lookup"><span data-stu-id="5f094-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="5f094-170">Используемый пример.</span><span class="sxs-lookup"><span data-stu-id="5f094-170">The example that is used.</span></span> <span data-ttu-id="5f094-171">В нем вычисляется кратчайший путь между ID 1 и всеми другими идентификаторами в графе.</span><span class="sxs-lookup"><span data-stu-id="5f094-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="5f094-172">Головной узел кластера.</span><span class="sxs-lookup"><span data-stu-id="5f094-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="5f094-173">Формат входных данных.</span><span class="sxs-lookup"><span data-stu-id="5f094-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="5f094-174">Файл входных данных.</span><span class="sxs-lookup"><span data-stu-id="5f094-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="5f094-175">Формат выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5f094-175">The output format.</span></span> <span data-ttu-id="5f094-176">В данном примере — ИД и значение в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="5f094-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="5f094-177">Расположение выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5f094-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="5f094-178">Количество используемых рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="5f094-178">The number of workers to use.</span></span> <span data-ttu-id="5f094-179">В этом примере — 2.</span><span class="sxs-lookup"><span data-stu-id="5f094-179">In this example, 2.</span></span> |

    <span data-ttu-id="5f094-180">Дополнительные сведения об этих и других параметрах, которые используются в примерах Giraph, см. в [кратком руководстве по Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="5f094-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="5f094-181">После завершения задания результаты сохраняются в каталоге **/example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="5f094-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="5f094-182">Имена выходных файлов будут начинаться с **part-m-** и заканчиваться числом, указывающим номер файла (первый, второй и т. д.).</span><span class="sxs-lookup"><span data-stu-id="5f094-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="5f094-183">Чтобы просмотреть выходные данные, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f094-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="5f094-184">Результат должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5f094-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="5f094-185">Пример SimpleShortestPathComputation жестко запрограммирован для запуска с объекта ID 1 и поиска кратчайшего пути к другим объектам.</span><span class="sxs-lookup"><span data-stu-id="5f094-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="5f094-186">Выходные данные имеют следующий формат: `destination_id` и `distance`.</span><span class="sxs-lookup"><span data-stu-id="5f094-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="5f094-187">`distance` представляет собой значение переходов на пути между объектом ID 1 и целевым объектом ID.</span><span class="sxs-lookup"><span data-stu-id="5f094-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="5f094-188">При визуализации данных можно проверить результаты, проходя кратчайшие пути между ID 1 и всеми другими объектами.</span><span class="sxs-lookup"><span data-stu-id="5f094-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="5f094-189">Кратчайший путь между ID 1 и ID 4 — это 5.</span><span class="sxs-lookup"><span data-stu-id="5f094-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="5f094-190">Это значение представляет собой общее расстояние между объектами <span style="color:orange">ID 1 и ID 3</span> и между объектами <span style="color:red">ID 3 и ID 4</span>.</span><span class="sxs-lookup"><span data-stu-id="5f094-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Представление объектов в виде кругов с кратчайшими путями между ними](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="5f094-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f094-192">Next steps</span></span>

* <span data-ttu-id="5f094-193">[Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5f094-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="5f094-194">[Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5f094-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
