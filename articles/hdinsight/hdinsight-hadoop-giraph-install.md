---
title: "Установка и использование Giraph для кластеров Hadoop в HDInsight — Azure | Документы Майкрософт"
description: "Дополнительные сведения о настройке кластера HDInsight с Giraph и использование Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="433f0-103">Установка и использование Giraph в кластерах HDInsight под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="433f0-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="433f0-104">Научитесь настраивать кластер HDInsight на основе Windows с Giraph с помощью сценария действия и использовать Giraph для обработки диаграмм больших объемов.</span><span class="sxs-lookup"><span data-stu-id="433f0-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="433f0-105">Сведения об использовании Giraph с кластером под управлением Linux см. в статье [Установка Giraph в кластерах HDInsight Hadoop и использование Giraph для обработки диаграмм больших объемов](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="433f0-106">Шаги, описанные в этом документе, можно применять только к кластерам HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="433f0-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="433f0-107">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="433f0-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="433f0-108">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="433f0-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="433f0-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="433f0-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="433f0-110">Сведения об установке Giraph в кластере под управлением Linux см. в статье [Установка Giraph в кластерах HDInsight Hadoop и использование Giraph для обработки диаграмм больших объемов](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="433f0-111">Giraph можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *действием скрипта*.</span><span class="sxs-lookup"><span data-stu-id="433f0-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="433f0-112">Пример скрипта для установки Giraph в кластере HDInsight доступен в большом двоичном объекте службы хранилища Azure (доступ только для чтения): [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="433f0-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="433f0-113">Пример скрипта работает только с кластером HDInsight версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="433f0-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="433f0-114">Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="433f0-115">**Связанные статьи**</span><span class="sxs-lookup"><span data-stu-id="433f0-115">**Related articles**</span></span>

* [<span data-ttu-id="433f0-116">Установка Giraph на кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="433f0-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="433f0-117">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="433f0-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="433f0-118">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="433f0-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="433f0-119">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="433f0-120">Что такое Giraph?</span><span class="sxs-lookup"><span data-stu-id="433f0-120">What is Giraph?</span></span>
<span data-ttu-id="433f0-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> позволяет выполнять обработку графов с использованием Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="433f0-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="433f0-122">Графы моделируют взаимоотношения между объектами, такие как подключения между маршрутизаторами в большой сети, подобной Интернету, или взаимоотношения между людьми в социальных сетях (иногда называется социальным графом).</span><span class="sxs-lookup"><span data-stu-id="433f0-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="433f0-123">Обработка графов дает возможность делать выводы о взаимоотношениях объектов в графе, таких как:</span><span class="sxs-lookup"><span data-stu-id="433f0-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="433f0-124">определение потенциальных друзей на основе текущих взаимоотношений;</span><span class="sxs-lookup"><span data-stu-id="433f0-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="433f0-125">определение кратчайшего маршрута между двумя компьютерами в сети;</span><span class="sxs-lookup"><span data-stu-id="433f0-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="433f0-126">вычисление ранга страницы для веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="433f0-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="433f0-127">Установка Giraph с помощью портала</span><span class="sxs-lookup"><span data-stu-id="433f0-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="433f0-128">Начните создание кластера с помощью параметра **Настраиваемое создание**, как описано в статье [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="433f0-129">На странице **Действия скрипта** мастера щелкните **Добавить действие скрипта** для предоставления сведений о данном действии скрипта, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="433f0-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="433f0-130">![Использование действия сценария для настройки кластера](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Использование действия сценария для настройки кластера")</span><span class="sxs-lookup"><span data-stu-id="433f0-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="433f0-131">Свойство</span><span class="sxs-lookup"><span data-stu-id="433f0-131">Property</span></span></th><th><span data-ttu-id="433f0-132">Значение</span><span class="sxs-lookup"><span data-stu-id="433f0-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="433f0-133">Имя</span><span class="sxs-lookup"><span data-stu-id="433f0-133">Name</span></span></td>
            <td><span data-ttu-id="433f0-134">Укажите имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="433f0-134">Specify a name for the script action.</span></span> <span data-ttu-id="433f0-135">Например, <b>Установка Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="433f0-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="433f0-136">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="433f0-136">Script URI</span></span></td>
            <td><span data-ttu-id="433f0-137">Укажите универсальный идентификатор ресурса (URI) для сценария, который вызывается для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="433f0-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="433f0-138">Например, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="433f0-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="433f0-139">Тип узла</span><span class="sxs-lookup"><span data-stu-id="433f0-139">Node Type</span></span></td>
            <td><span data-ttu-id="433f0-140">Укажите узлы, на которых выполняется сценарий настройки.</span><span class="sxs-lookup"><span data-stu-id="433f0-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="433f0-141">Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).</span><span class="sxs-lookup"><span data-stu-id="433f0-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="433f0-142">Параметры</span><span class="sxs-lookup"><span data-stu-id="433f0-142">Parameters</span></span></td>
            <td><span data-ttu-id="433f0-143">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="433f0-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="433f0-144">Скрипт для установки Giraph не требует никаких параметров, поэтому можно оставить это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="433f0-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="433f0-145">Можно добавить несколько действий сценария для установки нескольких компонентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="433f0-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="433f0-146">После добавления скриптов щелкните флажок, чтобы начать создание кластера.</span><span class="sxs-lookup"><span data-stu-id="433f0-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="433f0-147">Использование Giraph</span><span class="sxs-lookup"><span data-stu-id="433f0-147">Use Giraph</span></span>
<span data-ttu-id="433f0-148">Мы используем пример SimpleShortestPathsComputation, который демонстрирует базовую реализацию <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> для поиска кратчайшего пути между объектами графа.</span><span class="sxs-lookup"><span data-stu-id="433f0-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="433f0-149">Выполните следующие действия, чтобы отправить данные и JAR-файл примера, запустить задание с использованием примера SimpleShortestPathsComputation, а затем просмотреть результаты.</span><span class="sxs-lookup"><span data-stu-id="433f0-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="433f0-150">Передайте образец файла данных в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="433f0-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="433f0-151">На локальной рабочей станции создайте новый файл с именем **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="433f0-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="433f0-152">В нем должны присутствовать следующие строки.</span><span class="sxs-lookup"><span data-stu-id="433f0-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="433f0-153">Отправьте файл tiny_graph.txt в основное хранилище для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="433f0-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="433f0-154">Указания по отправке данных см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="433f0-155">Эти данные описывают взаимоотношения между объектами в направленном графе с использованием формата [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span><span class="sxs-lookup"><span data-stu-id="433f0-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="433f0-156">Каждая строка представляет взаимоотношение между объектом **source\_id** и одним или несколькими объектами **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="433f0-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="433f0-157">Значение **edge\_value** (или вес) можно представить себе как силу или расстояние подключения между **source_id** и **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="433f0-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="433f0-158">В визуальной форме и с использованием значения (или веса) в качестве расстояния между объектами указанные выше данные могут выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="433f0-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt начерчен в виде кругов с линиями различной длины между](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="433f0-160">Запустите пример SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="433f0-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="433f0-161">Воспользуйтесь следующими командлетами Azure PowerShell для запуска этого примера, используя файл tiny_graph.txt в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="433f0-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="433f0-162">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="433f0-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="433f0-163">В описанных в этом документе инструкциях используются новые командлеты HDInsight, которые работают с Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="433f0-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="433f0-164">Чтобы установить последнюю версию Azure PowerShell, выполните действия из статьи [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="433f0-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="433f0-165">Если у вас есть сценарии, в которые нужно добавить новые командлеты, работающие с Azure Resource Manager, см. статью [Переход к средствам разработки на основе Azure Resource Manager для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="433f0-166">В приведенном выше примере замените **clustername** именем кластера HDInsight, где установлен Giraph.</span><span class="sxs-lookup"><span data-stu-id="433f0-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="433f0-167">Просмотрите результаты.</span><span class="sxs-lookup"><span data-stu-id="433f0-167">View the results.</span></span> <span data-ttu-id="433f0-168">Когда задание будет завершено, результаты будут храниться в двух выходных файлах в папке **wasb:///example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="433f0-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="433f0-169">Эти файлы называются **part-m-00001** и **part-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="433f0-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="433f0-170">Выполните следующие действия, чтобы скачать и просмотреть выходные данные.</span><span class="sxs-lookup"><span data-stu-id="433f0-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="433f0-171">В результате создается структура каталога **example/output/shortestpaths** в текущем каталоге на рабочей станции, а выходные файлы скачиваются в это расположение.</span><span class="sxs-lookup"><span data-stu-id="433f0-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="433f0-172">Используйте командлет **Cat**, чтобы отобразить содержимое файлов.</span><span class="sxs-lookup"><span data-stu-id="433f0-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="433f0-173">Результат должен выглядеть аналогично следующему:</span><span class="sxs-lookup"><span data-stu-id="433f0-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="433f0-174">Пример SimpleShortestPathComputation жестко запрограммирован для запуска с объекта ID 1 и поиска кратчайшего пути к другим объектам.</span><span class="sxs-lookup"><span data-stu-id="433f0-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="433f0-175">Таким образом, выходные данные должны считываться как `destination_id distance`, где расстояние представляет собой значение (или вес) переходов на пути между объектом ID 1 и целевым объектом ID.</span><span class="sxs-lookup"><span data-stu-id="433f0-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="433f0-176">При визуализации можно проверить результаты, проходя кратчайшие пути между ID 1 и всеми другими объектами.</span><span class="sxs-lookup"><span data-stu-id="433f0-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="433f0-177">Обратите внимание, что кратчайший путь между ID 1 и ID 4 — это 5.</span><span class="sxs-lookup"><span data-stu-id="433f0-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="433f0-178">Это общее расстояние между объектами <span style="color:orange">ID 1 и ID 3</span> и между объектами <span style="color:red">ID 3 и ID 4</span>.</span><span class="sxs-lookup"><span data-stu-id="433f0-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Представление объектов в виде кругов с кратчайшими путями между ними](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="433f0-180">Установка Giraph с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="433f0-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="433f0-181">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="433f0-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="433f0-182">В этом примере показано, как установить Spark с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="433f0-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="433f0-183">Необходимо изменить сценарий для использования [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="433f0-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="433f0-184">Установка Giraph с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="433f0-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="433f0-185">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="433f0-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="433f0-186">В этом примере показано, как установить Spark с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="433f0-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="433f0-187">Необходимо изменить сценарий для использования [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="433f0-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="433f0-188">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="433f0-188">See also</span></span>
* [<span data-ttu-id="433f0-189">Установка Giraph на кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="433f0-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="433f0-190">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="433f0-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="433f0-191">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="433f0-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="433f0-192">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="433f0-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="433f0-193">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.</span><span class="sxs-lookup"><span data-stu-id="433f0-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="433f0-194">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. Пример действия сценария для установки R.</span><span class="sxs-lookup"><span data-stu-id="433f0-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="433f0-195">[Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install.md) — пример действия скрипта для установки Solr.</span><span class="sxs-lookup"><span data-stu-id="433f0-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
