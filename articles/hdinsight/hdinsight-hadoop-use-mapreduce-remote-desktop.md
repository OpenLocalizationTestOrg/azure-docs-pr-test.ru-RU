---
title: "Использование MapReduce и удаленного рабочего стола с Hadoop в HDInsight — Azure | Документы Майкрософт"
description: "Информация об использовании удаленного рабочего стола для подключения к Hadoop в HDInsight и выполнения заданий MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: b56674857b013f9bb3d4dd4b6e97b34e0a97b1b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="43971-103">Использование MapReduce в Hadoop в HDInsight с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="43971-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="43971-104">В этой статье вы узнаете, как подключиться к Hadoop в кластере HDInsight с помощью удаленного рабочего стола, а затем выполнить задания MapReduce с помощью команды Hadoop.</span><span class="sxs-lookup"><span data-stu-id="43971-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43971-105">Удаленный рабочий стол доступен только в кластерах HDInsight на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="43971-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="43971-106">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="43971-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="43971-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="43971-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="43971-108">При использовании HDInsight 3.4 или более поздней версии см. сведения о подключении к кластеру HDInsight и выполнении заданий MapReduce: [Использование MapReduce с Hadoop в HDInsight с помощью SSH](hdinsight-hadoop-use-mapreduce-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="43971-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="43971-109"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="43971-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="43971-110">Чтобы выполнить действия, описанные в этой статье, необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="43971-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="43971-111">Кластер HDInsight на платформе Windows (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="43971-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="43971-112">Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="43971-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="43971-113"><a id="connect"></a>Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="43971-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="43971-114">Запустите протокол удаленного рабочего стола для кластера HDInsight, а затем выполните подключение, следуя инструкциям раздела [Подключение к кластерам HDInsight с использованием RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="43971-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="43971-115"><a id="hadoop"></a>Использование команды Hadoop</span><span class="sxs-lookup"><span data-stu-id="43971-115"><a id="hadoop"></a>Use the Hadoop command</span></span>
<span data-ttu-id="43971-116">После подключения к рабочему столу кластера HDInsight сделайте следующее, чтобы выполнить задание MapReduce с помощью команды Hadoop:</span><span class="sxs-lookup"><span data-stu-id="43971-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="43971-117">На рабочем столе HDInsight запустите **командную строку Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="43971-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="43971-118">Откроется новое окно командной строки в каталоге **c:\apps\dist\hadoop-&lt;номер_версии>**.</span><span class="sxs-lookup"><span data-stu-id="43971-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43971-119">При обновлении Hadoop номер версии изменяется.</span><span class="sxs-lookup"><span data-stu-id="43971-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="43971-120">Для поиска пути можно использовать переменную среды **HADOOP_HOME**.</span><span class="sxs-lookup"><span data-stu-id="43971-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="43971-121">Например, `cd %HADOOP_HOME%` изменит каталоги на каталог Hadoop без необходимости знать номер версии.</span><span class="sxs-lookup"><span data-stu-id="43971-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="43971-122">Чтобы выполнить пример задания MapReduce с помощью команды **Hadoop** , используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43971-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="43971-123">При этом запустится класс **wordcount**, содержащийся в текущем каталоге в файле **hadoop-mapreduce-examples.jar**.</span><span class="sxs-lookup"><span data-stu-id="43971-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="43971-124">В качестве входных данных он использует документ **wasb://example/data/gutenberg/davinci.txt**, а выходные данные сохраняются в **wasb:///example/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="43971-124">As input, it uses the **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43971-125">Дополнительные сведения об этом задании MapReduce и данные для примера см. в разделе <a href="hdinsight-use-mapreduce.md">Использование MapReduce в HDInsight в Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="43971-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="43971-126">Задание выдает информацию о ходе обработки, а по завершении задания возвращает информацию, аналогичную приведенной ниже:</span><span class="sxs-lookup"><span data-stu-id="43971-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="43971-127">После завершения используйте следующую команду, чтобы вывести список выходных файлов, сохраненных в **wasb://example/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="43971-127">When the job is complete, use the following command to list the output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="43971-128">Должно отобразиться два файла: **_SUCCESS** и **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="43971-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="43971-129">Файл **part-r-00000** содержит выходные данные этого задания.</span><span class="sxs-lookup"><span data-stu-id="43971-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43971-130">Некоторые задания MapReduce могут разделять результаты на несколько файлов **part-r-№№№№№** .</span><span class="sxs-lookup"><span data-stu-id="43971-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="43971-131">В этом случае используйте суффикс №№№№№, чтобы определить порядок файлов.</span><span class="sxs-lookup"><span data-stu-id="43971-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="43971-132">Чтобы просмотреть выходные данные, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43971-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="43971-133">При этом отобразится список слов, содержащихся в файле **wasb://example/data/gutenberg/davinci.txt**, а также количество вхождений каждого из них.</span><span class="sxs-lookup"><span data-stu-id="43971-133">This displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="43971-134">Ниже приведен пример данных, которые будут содержаться в файле.</span><span class="sxs-lookup"><span data-stu-id="43971-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="43971-135"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="43971-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="43971-136">Как видите, команда Hadoop позволяет с легкостью выполнять задания MapReduce в кластере HDInsight и просматривать выходные данные задания.</span><span class="sxs-lookup"><span data-stu-id="43971-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="43971-137"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43971-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="43971-138">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="43971-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="43971-139">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="43971-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="43971-140">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="43971-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="43971-141">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="43971-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="43971-142">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="43971-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
