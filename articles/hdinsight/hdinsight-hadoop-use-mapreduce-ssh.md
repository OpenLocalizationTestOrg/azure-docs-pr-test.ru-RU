---
title: "aaaMapReduce и SSH-подключения на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как SSH toouse toorun MapReduce заданий с помощью Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="75d89-103">Использование MapReduce с Hadoop в HDInsight с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="75d89-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="75d89-104">Узнайте, как задания toosubmit MapReduce tooHDInsight подключения Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="75d89-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="75d89-105">Если вы уже знакомы с использованием Hadoop на основе Linux серверы, но — новый tooHDInsight см [HDInsight под управлением Linux советы](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="75d89-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="75d89-106"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="75d89-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="75d89-107">Кластер HDInsight на основе Linux (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="75d89-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="75d89-108">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="75d89-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="75d89-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="75d89-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="75d89-110">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="75d89-110">An SSH client.</span></span> <span data-ttu-id="75d89-111">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="75d89-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="75d89-112"><a id="ssh"></a>Подключение по SSH</span><span class="sxs-lookup"><span data-stu-id="75d89-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="75d89-113">Подключите кластер toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="75d89-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="75d89-114">Например, следующая команда hello подключается tooa кластер с именем **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="75d89-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="75d89-115">**При использовании ключа сертификата для проверки подлинности SSH**, может потребоваться toospecify расположение hello hello закрытого ключа в системе клиента, например:</span><span class="sxs-lookup"><span data-stu-id="75d89-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="75d89-116">**Если использовать пароль для проверки подлинности SSH**, вам необходим пароль hello tooprovide при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="75d89-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="75d89-117">Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="75d89-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="75d89-118"><a id="hadoop"></a>Использование команд Hadoop</span><span class="sxs-lookup"><span data-stu-id="75d89-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="75d89-119">После toohello подключенных кластера HDInsight, используйте hello следующая команда toostart задание MapReduce:</span><span class="sxs-lookup"><span data-stu-id="75d89-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="75d89-120">Эта команда запускает hello `wordcount` класс, который содержится в hello `hadoop-mapreduce-examples.jar` файла.</span><span class="sxs-lookup"><span data-stu-id="75d89-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="75d89-121">Она использует hello `/example/data/gutenberg/davinci.txt` документа в качестве входных и выходных данных хранится в `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="75d89-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75d89-122">Дополнительные сведения о MapReduce задания и hello данными из этого примера см. в разделе [используйте MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="75d89-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="75d89-123">Задание Hello выдает сведения при обработке, и возвращает сведения аналогичные toohello после текста, при завершении задания hello:</span><span class="sxs-lookup"><span data-stu-id="75d89-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="75d89-124">По завершении заданий hello используйте hello следующая команда toolist hello выходных файлов:</span><span class="sxs-lookup"><span data-stu-id="75d89-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="75d89-125">Эта команда отображает два файла — `_SUCCESS` и `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="75d89-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="75d89-126">Hello `part-r-00000` файл содержит hello выходные данные для этого задания.</span><span class="sxs-lookup"><span data-stu-id="75d89-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75d89-127">Некоторые задания MapReduce может разделить результаты hello в нескольких **часть r-###** файлов.</span><span class="sxs-lookup"><span data-stu-id="75d89-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="75d89-128">Если Да, использовать hello ### суффикс tooindicate hello порядок файлов hello.</span><span class="sxs-lookup"><span data-stu-id="75d89-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="75d89-129">Вывод tooview hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="75d89-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="75d89-130">Эта команда отображает список слов hello, содержащиеся в hello **wasb://example/data/gutenberg/davinci.txt** файл и hello число возникновений каждого слова.</span><span class="sxs-lookup"><span data-stu-id="75d89-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="75d89-131">Hello следующий текст является примером hello данные, содержащиеся в файле hello:</span><span class="sxs-lookup"><span data-stu-id="75d89-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="75d89-132"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="75d89-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="75d89-133">Как видите, Hadoop команды предоставляют простой способ toorun задания MapReduce в кластер HDInsight и просмотр выходных данных задания hello.</span><span class="sxs-lookup"><span data-stu-id="75d89-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="75d89-134"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75d89-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="75d89-135">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="75d89-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="75d89-136">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75d89-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="75d89-137">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="75d89-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="75d89-138">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75d89-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="75d89-139">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="75d89-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
