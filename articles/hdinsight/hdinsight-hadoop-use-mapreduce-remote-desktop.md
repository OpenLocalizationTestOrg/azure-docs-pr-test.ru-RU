---
title: "aaaMapReduce и удаленного рабочего стола с Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как tooHadoop tooconnect toouse удаленного рабочего стола на HDInsight и выполнения заданий MapReduce."
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
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="1323c-103">Использование MapReduce в Hadoop в HDInsight с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="1323c-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="1323c-104">В этой статье будет узнать, как кластер tooconnect tooa Hadoop в HDInsight с помощью удаленного рабочего стола и запустите задания MapReduce с помощью команды Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="1323c-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1323c-105">Удаленный рабочий стол доступен только в кластерах HDInsight на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="1323c-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1323c-106">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="1323c-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1323c-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1323c-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="1323c-108">Для HDInsight 3.4 или выше в разделе [используйте MapReduce с SSH](hdinsight-hadoop-use-mapreduce-ssh.md) сведения о подключении кластера HDInsight toohello и выполнения заданий MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1323c-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="1323c-109"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1323c-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="1323c-110">в этой статье инструкциям toocomplete hello, вам потребуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1323c-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="1323c-111">Кластер HDInsight на платформе Windows (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="1323c-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="1323c-112">Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="1323c-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="1323c-113"><a id="connect"></a>Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="1323c-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="1323c-114">Включить удаленный рабочий стол для кластера HDInsight hello, а затем соедините tooit в соответствии с инструкциями hello в [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="1323c-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="1323c-115"><a id="hadoop"></a>Команда Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="1323c-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="1323c-116">Подключенных toohello рабочий стол для кластера HDInsight hello, используйте следующие шаги toorun задание MapReduce с помощью команды Hadoop hello hello:</span><span class="sxs-lookup"><span data-stu-id="1323c-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="1323c-117">С рабочего стола HDInsight hello, запустите hello **командной строки Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="1323c-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="1323c-118">Это открывает новую командную строку в hello **c:\apps\dist\hadoop-&lt;номер версии >** каталога.</span><span class="sxs-lookup"><span data-stu-id="1323c-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1323c-119">номер версии Hello изменяются по мере обновления Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1323c-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="1323c-120">Hello **HADOOP_HOME** переменной среды может быть путь используется toofind hello.</span><span class="sxs-lookup"><span data-stu-id="1323c-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="1323c-121">Например `cd %HADOOP_HOME%` изменения каталоги toohello Hadoop в каталоге, не требуя номер версии tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="1323c-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="1323c-122">toouse hello **Hadoop** toorun задание MapReduce пример команды, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1323c-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="1323c-123">Запустится hello **wordcount** класс, который содержится в hello **mapreduce-hadoop-examples.jar** файл в текущем каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="1323c-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="1323c-124">В качестве входного, он использует hello **wasb://example/data/gutenberg/davinci.txt** хранится документ и выход по: **wasb: / / / пример/данных/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="1323c-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1323c-125">Дополнительные сведения о MapReduce задания и hello данными из этого примера см. в разделе <a href="hdinsight-use-mapreduce.md">используйте MapReduce в HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="1323c-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="1323c-126">Задание Hello выдает сведения, как его обработки, и возвращает аналогичные toohello следующие сведения при завершении задания hello:</span><span class="sxs-lookup"><span data-stu-id="1323c-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="1323c-127">По завершении задания hello использовать hello, следующая команда toolist hello выходные файлы, хранящиеся в **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="1323c-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="1323c-128">Должно отобразиться два файла: **_SUCCESS** и **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="1323c-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="1323c-129">Hello **часть r-00000** файл содержит hello выходные данные для этого задания.</span><span class="sxs-lookup"><span data-stu-id="1323c-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1323c-130">Некоторые задания MapReduce может разделить результаты hello в нескольких **часть r-###** файлов.</span><span class="sxs-lookup"><span data-stu-id="1323c-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="1323c-131">Если Да, использовать hello ### суффикс tooindicate hello порядок файлов hello.</span><span class="sxs-lookup"><span data-stu-id="1323c-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="1323c-132">Вывод tooview hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1323c-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="1323c-133">Это список hello слов, которые содержатся в hello **wasb://example/data/gutenberg/davinci.txt** файла вместе с hello число возникновений каждого слова.</span><span class="sxs-lookup"><span data-stu-id="1323c-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="1323c-134">Hello ниже приведен пример hello данных, которые будут содержаться в файле hello:</span><span class="sxs-lookup"><span data-stu-id="1323c-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="1323c-135"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="1323c-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="1323c-136">Как видите, hello команда Hadoop, посвященная toorun простой способ задания MapReduce кластер HDInsight и просмотр выходных данных задания hello.</span><span class="sxs-lookup"><span data-stu-id="1323c-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="1323c-137"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1323c-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="1323c-138">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1323c-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="1323c-139">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1323c-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1323c-140">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1323c-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1323c-141">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1323c-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1323c-142">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1323c-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
