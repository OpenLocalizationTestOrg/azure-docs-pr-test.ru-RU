---
title: "Использование MapReduce и подключения SSH с Hadoop в HDInsight — Azure | Документы Майкрософт"
description: "Информация об использовании SSH для выполнения заданий MapReduce с помощью Hadoop в HDInsight."
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
ms.openlocfilehash: eaf6278f97cd5ddd7e049ff4745181f39d7949a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="26f71-103">Использование MapReduce с Hadoop в HDInsight с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="26f71-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="26f71-104">Узнайте, как отправлять задания MapReduce в HDInsight с помощью подключения SSH.</span><span class="sxs-lookup"><span data-stu-id="26f71-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="26f71-105">Если вы уже знаете, как использовать серверы Hadoop на платформе Linux, но не знакомы с HDInsight, см. статью [Сведения об использовании HDInsight в Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="26f71-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="26f71-106"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="26f71-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="26f71-107">Кластер HDInsight на основе Linux (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="26f71-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="26f71-108">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="26f71-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="26f71-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="26f71-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="26f71-110">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="26f71-110">An SSH client.</span></span> <span data-ttu-id="26f71-111">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="26f71-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="26f71-112"><a id="ssh"></a>Подключение по SSH</span><span class="sxs-lookup"><span data-stu-id="26f71-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="26f71-113">Подключитесь к кластеру с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="26f71-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="26f71-114">Например, следующая команда позволяет подключиться к кластеру с именем **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="26f71-114">For example, the following command connects to a cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="26f71-115">**Если вы используете ключ сертификата для аутентификации SSH**, возможно, потребуется указать расположение закрытого ключа в клиентской системе. Пример:</span><span class="sxs-lookup"><span data-stu-id="26f71-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="26f71-116">**Если вы используете пароль для аутентификации SSH**, его необходимо ввести при запросе.</span><span class="sxs-lookup"><span data-stu-id="26f71-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="26f71-117">Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="26f71-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="26f71-118"><a id="hadoop"></a>Использование команд Hadoop</span><span class="sxs-lookup"><span data-stu-id="26f71-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="26f71-119">После подключения к кластеру HDInsight используйте следующую команду, чтобы запустить задание MapReduce:</span><span class="sxs-lookup"><span data-stu-id="26f71-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="26f71-120">Эта команда запускает класс `wordcount`, который содержится в файле `hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="26f71-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="26f71-121">Она использует документ `/example/data/gutenberg/davinci.txt` в качестве входных данных, а выходные данные хранятся в `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="26f71-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="26f71-122">Дополнительную информацию об этом задании MapReduce и примере данных см. в разделе [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="26f71-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="26f71-123">Задание выдает информацию о ходе обработки, а по завершении задания возвращает информацию, аналогичную приведенной ниже:</span><span class="sxs-lookup"><span data-stu-id="26f71-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="26f71-124">По завершении задания воспользуйтесь следующей командой, чтобы просмотреть выходные файлы:</span><span class="sxs-lookup"><span data-stu-id="26f71-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="26f71-125">Эта команда отображает два файла — `_SUCCESS` и `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="26f71-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="26f71-126">Файл `part-r-00000` содержит выходные данные этого задания.</span><span class="sxs-lookup"><span data-stu-id="26f71-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="26f71-127">Некоторые задания MapReduce могут разделять результаты на несколько файлов **part-r-№№№№№** .</span><span class="sxs-lookup"><span data-stu-id="26f71-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="26f71-128">В этом случае используйте суффикс №№№№№, чтобы определить порядок файлов.</span><span class="sxs-lookup"><span data-stu-id="26f71-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="26f71-129">Чтобы просмотреть выходные данные, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="26f71-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="26f71-130">Она отобразит список слов, содержащихся в файле **wasb://example/data/gutenberg/davinci.txt**, а также число вхождений каждого из них.</span><span class="sxs-lookup"><span data-stu-id="26f71-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="26f71-131">Ниже приведен пример данных, содержащихся в файле.</span><span class="sxs-lookup"><span data-stu-id="26f71-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="26f71-132"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="26f71-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="26f71-133">Как видите, команды Hadoop позволяют с легкостью выполнять задания MapReduce в кластере HDInsight и просматривать выходные данные задания.</span><span class="sxs-lookup"><span data-stu-id="26f71-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="26f71-134"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26f71-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="26f71-135">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="26f71-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="26f71-136">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f71-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="26f71-137">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="26f71-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="26f71-138">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f71-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="26f71-139">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="26f71-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
