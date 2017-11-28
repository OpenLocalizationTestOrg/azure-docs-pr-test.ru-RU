---
title: "кластеры aaaInstall и используйте Giraph на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластер с Giraph и как toouse Giraph."
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
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="3f454-103">Установка и использование Giraph в кластерах HDInsight под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="3f454-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="3f454-104">Узнайте, как toocustomize Windows на основе кластеров HDInsight с Giraph, с помощью действия скрипта и как toouse Giraph tooprocess крупномасштабных диаграмм.</span><span class="sxs-lookup"><span data-stu-id="3f454-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="3f454-105">Сведения об использовании Giraph с кластером под управлением Linux см. в статье [Установка Giraph в кластерах HDInsight Hadoop и использование Giraph для обработки диаграмм больших объемов](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f454-106">Hello шагов в этот документ корректно работать только с кластерами HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="3f454-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="3f454-107">Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows.</span><span class="sxs-lookup"><span data-stu-id="3f454-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="3f454-108">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="3f454-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3f454-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3f454-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="3f454-110">Сведения о том, как tooinstall Giraph в кластере HDInsight под управлением Linux. в разделе [Giraph установить в кластерах HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="3f454-111">Giraph можно установить в кластере любого типа (Hadoop, Storm, HBase, Spark) в HDInsight в Azure, воспользовавшись *действием скрипта*.</span><span class="sxs-lookup"><span data-stu-id="3f454-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="3f454-112">Образец сценария tooinstall Giraph в кластере HDInsight доступна из большого двоичного объекта хранилища Azure только для чтения, в [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="3f454-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="3f454-113">Пример сценария Hello работает только с кластера HDInsight версии 3.1.</span><span class="sxs-lookup"><span data-stu-id="3f454-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="3f454-114">Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="3f454-115">**Связанные статьи**</span><span class="sxs-lookup"><span data-stu-id="3f454-115">**Related articles**</span></span>

* [<span data-ttu-id="3f454-116">Установка Giraph на кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="3f454-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="3f454-117">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3f454-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="3f454-118">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="3f454-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="3f454-119">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="3f454-120">Что такое Giraph?</span><span class="sxs-lookup"><span data-stu-id="3f454-120">What is Giraph?</span></span>
<span data-ttu-id="3f454-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3f454-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="3f454-122">Графы моделирования связей между объектами, например hello соединения между маршрутизаторами в больших сетях, как Интернет, hello или связи между пользователями в социальных сетях (который иногда ссылается tooas социального графа).</span><span class="sxs-lookup"><span data-stu-id="3f454-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="3f454-123">Обработка Graph позволяет tooreason о hello связей между объектами в граф, такие как:</span><span class="sxs-lookup"><span data-stu-id="3f454-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="3f454-124">определение потенциальных друзей на основе текущих взаимоотношений;</span><span class="sxs-lookup"><span data-stu-id="3f454-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="3f454-125">Определение hello кратчайший маршрут между двумя компьютерами в сети.</span><span class="sxs-lookup"><span data-stu-id="3f454-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="3f454-126">Вычисление ранга hello страницы веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="3f454-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="3f454-127">Установка Giraph с помощью портала</span><span class="sxs-lookup"><span data-stu-id="3f454-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="3f454-128">Начать создание кластера с помощью hello **НАСТРАИВАЕМОЕ создание** параметра, как описано в разделе [кластеров создать Hadoop в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="3f454-129">На hello **действия скрипта** страница приветствия мастера нажмите кнопку **добавьте действия скрипта** tooprovide сведений о hello действие скрипта, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3f454-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="3f454-130">![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize действия скрипта для использования кластера")</span><span class="sxs-lookup"><span data-stu-id="3f454-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="3f454-131">Свойство</span><span class="sxs-lookup"><span data-stu-id="3f454-131">Property</span></span></th><th><span data-ttu-id="3f454-132">Значение</span><span class="sxs-lookup"><span data-stu-id="3f454-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="3f454-133">Имя</span><span class="sxs-lookup"><span data-stu-id="3f454-133">Name</span></span></td>
            <td><span data-ttu-id="3f454-134">Укажите имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-134">Specify a name for hello script action.</span></span> <span data-ttu-id="3f454-135">Например, <b>Установка Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="3f454-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="3f454-136">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="3f454-136">Script URI</span></span></td>
            <td><span data-ttu-id="3f454-137">Укажите сценарий toohello универсальный код ресурса (URI) hello, вызванный toocustomize hello кластера.</span><span class="sxs-lookup"><span data-stu-id="3f454-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="3f454-138">Например, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i>.</span><span class="sxs-lookup"><span data-stu-id="3f454-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="3f454-139">Тип узла</span><span class="sxs-lookup"><span data-stu-id="3f454-139">Node Type</span></span></td>
            <td><span data-ttu-id="3f454-140">Укажите hello узлов, на которых выполняется скрипт настройки hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="3f454-141">Вы можете выбрать одно из трех значений: <b>Все узлы</b>, <b>Только головные узлы</b> или <b>Worker nodes only</b> (Только рабочие узлы).</span><span class="sxs-lookup"><span data-stu-id="3f454-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="3f454-142">Параметры</span><span class="sxs-lookup"><span data-stu-id="3f454-142">Parameters</span></span></td>
            <td><span data-ttu-id="3f454-143">Укажите параметры hello, если это требуется для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="3f454-144">сценарий Hello tooinstall Giraph параметры не требуются, поэтому это поле можно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="3f454-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="3f454-145">Можно добавить несколько компонентов несколько tooinstall действие сценария в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="3f454-146">После добавления скриптов hello, щелкните флажок toostart hello, для создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="3f454-147">Использование Giraph</span><span class="sxs-lookup"><span data-stu-id="3f454-147">Use Giraph</span></span>
<span data-ttu-id="3f454-148">Мы используем hello SimpleShortestPathsComputation пример toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> реализацию для обнаружения hello кратчайшего пути между объектами в граф.</span><span class="sxs-lookup"><span data-stu-id="3f454-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="3f454-149">Используйте следующие шаги tooupload hello образец данных и hello образец JAR-файл, запустите задание, используя пример SimpleShortestPathsComputation hello и просмотр результатов hello hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="3f454-150">Отправьте tooAzure файла данных образец хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3f454-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="3f454-151">На локальной рабочей станции создайте новый файл с именем **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="3f454-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="3f454-152">Она должна содержать hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="3f454-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="3f454-153">Отправьте hello tiny_graph.txt файл toohello основного хранилища для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3f454-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="3f454-154">Дополнительные сведения о данных tooupload. в разделе [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="3f454-155">Эти данные описывает связь между объектами в направленный граф, используя формат hello [источника\_идентификатор, источник\_значение, [[dest\_id], [edge\_значение],...]]. Каждая строка представляет взаимоотношение между объектом **source\_id** и одним или несколькими объектами **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="3f454-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="3f454-156">Hello **edge\_значение** (или вес) можно рассматривать как стойкость hello или расстояние hello соединения между **source_id** и **dest\_идентификатор**.</span><span class="sxs-lookup"><span data-stu-id="3f454-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="3f454-157">Рисования, используя значение hello (или вес) в качестве hello расстояния между объектами, hello выше данных может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3f454-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt начерчен в виде кругов с линиями различной длины между](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="3f454-159">Запустите пример SimpleShortestPathsComputation hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="3f454-160">Используйте следующий пример hello toorun командлетов Azure PowerShell с помощью файла tiny_graph.txt hello в качестве входных данных hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3f454-161">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3f454-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="3f454-162">шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3f454-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="3f454-163">Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f454-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="3f454-164">При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="3f454-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="3f454-165">В приведенном выше примере hello, замените **clustername** с hello имя кластера HDInsight с Giraph установлен.</span><span class="sxs-lookup"><span data-stu-id="3f454-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="3f454-166">Просмотр результатов hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-166">View hello results.</span></span> <span data-ttu-id="3f454-167">По завершении задания hello hello результаты будет храниться в двух файлах вывода в hello **wasb: / / / пример/out/shotestpaths** папки.</span><span class="sxs-lookup"><span data-stu-id="3f454-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="3f454-168">Привет, называются **часть m 00001 было указано** и **часть m-00002**.</span><span class="sxs-lookup"><span data-stu-id="3f454-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="3f454-169">Выполните следующие действия toodownload и просмотреть выходной hello hello.</span><span class="sxs-lookup"><span data-stu-id="3f454-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="3f454-170">Это создаст hello **пример, выходные данные или shortestpaths** структуру каталогов в текущем каталоге hello на рабочей станции и toothat файлы расположения для загрузки hello два выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3f454-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="3f454-171">Используйте hello **Cat** командлет toodisplay hello содержимое файлов hello:</span><span class="sxs-lookup"><span data-stu-id="3f454-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="3f454-172">Hello вывод должен выглядеть примерно следующие toohello:</span><span class="sxs-lookup"><span data-stu-id="3f454-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="3f454-173">Пример SimpleShortestPathComputation Hello является жестко заданный toostart с Идентификатором 1 объекта и поиска hello кратчайший путь tooother объектов.</span><span class="sxs-lookup"><span data-stu-id="3f454-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="3f454-174">Поэтому hello выходные данные должны читаться как `destination_id distance`, где расстояние — hello значение (или вес) границ hello пути между объектом с Идентификатором 1 и идентификатором hello объекта.</span><span class="sxs-lookup"><span data-stu-id="3f454-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="3f454-175">Визуализация это, можно проверить результаты hello, проходящих hello кратчайшего пути между Идентификатором 1 и других объектов.</span><span class="sxs-lookup"><span data-stu-id="3f454-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="3f454-176">Обратите внимание, что hello кратчайшего пути между 1 идентификатор и идентификатор 4 — 5.</span><span class="sxs-lookup"><span data-stu-id="3f454-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="3f454-177">Это hello общее расстояние между <span style="color:orange">идентификатор 1 и 3</span>, а затем <span style="color:red">идентификатор 3 и 4</span>.</span><span class="sxs-lookup"><span data-stu-id="3f454-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Представление объектов в виде кругов с кратчайшими путями между ними](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="3f454-179">Установка Giraph с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f454-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="3f454-180">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="3f454-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="3f454-181">Hello образце показано, как tooinstall Spark с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f454-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="3f454-182">Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="3f454-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="3f454-183">Установка Giraph с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="3f454-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="3f454-184">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="3f454-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="3f454-185">Hello образце показано, как tooinstall Spark с помощью пакета SDK для .NET "hello".</span><span class="sxs-lookup"><span data-stu-id="3f454-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="3f454-186">Требуется toocustomize hello сценарий toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="3f454-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="3f454-187">См. также</span><span class="sxs-lookup"><span data-stu-id="3f454-187">See also</span></span>
* [<span data-ttu-id="3f454-188">Установка Giraph на кластерах HDInsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="3f454-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="3f454-189">[Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-provision-clusters.md) — общие сведения о создании кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3f454-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="3f454-190">[Настройка кластера HDInsight с помощью действия сценария][hdinsight-cluster-customize]. Общая информация о настройке кластеров HDInsight с помощью действия сценария.</span><span class="sxs-lookup"><span data-stu-id="3f454-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="3f454-191">[Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="3f454-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="3f454-192">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. Пример действия сценария для установки Spark.</span><span class="sxs-lookup"><span data-stu-id="3f454-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="3f454-193">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. Пример действия сценария для установки R.</span><span class="sxs-lookup"><span data-stu-id="3f454-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="3f454-194">[Установка и использование Solr на кластерах HDInsight Hadoop](hdinsight-hadoop-solr-install.md) — пример действия скрипта для установки Solr.</span><span class="sxs-lookup"><span data-stu-id="3f454-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
