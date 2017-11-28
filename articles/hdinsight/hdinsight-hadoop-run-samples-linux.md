---
title: "Выполнение примеров Hadoop MapReduce в HDInsight — Azure | Документы Майкрософт"
description: "Начало работы с образцами MapReduce в файлах JAR, включенных в HDInsight. Для подключения к кластеру используйте SSH, после чего используйте команду Hadoop для запуска примеров заданий."
keywords: "пример jar-файла hadoop,примеры jar-файлов hadoop,примеры hadoop mapreduce,примеры mapreduce"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="99d6f-105">Выполнение примеров MapReduce, включенных в HDInsight</span><span class="sxs-lookup"><span data-stu-id="99d6f-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="99d6f-106">Узнайте, как выполнять примеры MapReduce, входящие в состав Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99d6f-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99d6f-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="99d6f-107">Prerequisites</span></span>

* <span data-ttu-id="99d6f-108">**Кластер HDInsight**. См. статью [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="99d6f-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="99d6f-109">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="99d6f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="99d6f-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="99d6f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="99d6f-111">**SSH-клиент**. Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="99d6f-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="99d6f-112">Примеры MapReduce</span><span class="sxs-lookup"><span data-stu-id="99d6f-112">The MapReduce examples</span></span>

<span data-ttu-id="99d6f-113">**Расположение**: примеры расположены в кластере HDInsight в `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="99d6f-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="99d6f-114">**Содержимое**. В архиве содержатся следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="99d6f-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="99d6f-115">`aggregatewordcount`: программа MapReduce для подсчета слов во входных файлах с использованием статистических выражений.</span><span class="sxs-lookup"><span data-stu-id="99d6f-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="99d6f-116">`aggregatewordhist`: программа MapReduce для создания гистограммы слов из входных файлов с использованием статистических выражений.</span><span class="sxs-lookup"><span data-stu-id="99d6f-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="99d6f-117">`bbp`: программа MapReduce для вычисления знаков числа π с использованием формулы Бэйли-Боруэйна-Плаффа.</span><span class="sxs-lookup"><span data-stu-id="99d6f-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="99d6f-118">`dbcount`: пример задания для подсчета журналов просмотра страниц, сохраненных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="99d6f-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="99d6f-119">`distbbp`: программа MapReduce для вычисления знаков числа π с использованием формулы ББП.</span><span class="sxs-lookup"><span data-stu-id="99d6f-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="99d6f-120">`grep`: программа MapReduce для подсчета вхождений регулярного выражения во входных данных.</span><span class="sxs-lookup"><span data-stu-id="99d6f-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="99d6f-121">`join`: задание для объединения сортированных наборов данных одного размера.</span><span class="sxs-lookup"><span data-stu-id="99d6f-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="99d6f-122">`multifilewc`: задание для подсчета слов в нескольких файлах.</span><span class="sxs-lookup"><span data-stu-id="99d6f-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="99d6f-123">`pentomino`: программа MapReduce для укладки фигур с целью поиска решений при игре в пентамино.</span><span class="sxs-lookup"><span data-stu-id="99d6f-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="99d6f-124">`pi`: программа MapReduce для расчета числа π по методу квази-Монте-Карло.</span><span class="sxs-lookup"><span data-stu-id="99d6f-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="99d6f-125">`randomtextwriter`: программа MapReduce для записи 10 ГБ случайных текстовых данных на узел.</span><span class="sxs-lookup"><span data-stu-id="99d6f-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="99d6f-126">`randomwriter`: программа MapReduce для записи 10 ГБ случайных данных на узел.</span><span class="sxs-lookup"><span data-stu-id="99d6f-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="99d6f-127">`secondarysort`: пример определения вторичной сортировки для этапа редукции.</span><span class="sxs-lookup"><span data-stu-id="99d6f-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="99d6f-128">`sort`: программа MapReduce для сортировки случайных данных.</span><span class="sxs-lookup"><span data-stu-id="99d6f-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="99d6f-129">`sudoku`: программа решения судоку.</span><span class="sxs-lookup"><span data-stu-id="99d6f-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="99d6f-130">`teragen`: создание данных для программы TeraSort.</span><span class="sxs-lookup"><span data-stu-id="99d6f-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="99d6f-131">`terasort`: выполнение программы TeraSort.</span><span class="sxs-lookup"><span data-stu-id="99d6f-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="99d6f-132">`teravalidate`: проверка результатов выполнения программы TeraSort.</span><span class="sxs-lookup"><span data-stu-id="99d6f-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="99d6f-133">`wordcount`: программа MapReduce для подсчета слов во входных файлах.</span><span class="sxs-lookup"><span data-stu-id="99d6f-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="99d6f-134">`wordmean`: программа MapReduce для подсчета средней длины слов во входных файлах.</span><span class="sxs-lookup"><span data-stu-id="99d6f-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="99d6f-135">`wordmedian`: программа MapReduce для подсчета средней длины слов по Смиту во входных файлах.</span><span class="sxs-lookup"><span data-stu-id="99d6f-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="99d6f-136">`wordstandarddeviation`: программа MapReduce для подсчета стандартного отклонения в длинах слов во входных файлах.</span><span class="sxs-lookup"><span data-stu-id="99d6f-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="99d6f-137">**Исходный код**: исходный код этих примеров расположен в кластере HDInsight в `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="99d6f-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="99d6f-138">`2.2.4.9-1` в пути соответствует версии платформы данных Hortonworks Data Platform для кластера HDInsight, которая может отличаться для вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="99d6f-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="99d6f-139">Запуск примера для подсчета слов</span><span class="sxs-lookup"><span data-stu-id="99d6f-139">Run the wordcount example</span></span>

1. <span data-ttu-id="99d6f-140">Подключитесь к HDInsight с помощью протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="99d6f-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="99d6f-141">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="99d6f-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="99d6f-142">В командной строке `username@#######:~$` введите следующую команду, чтобы вывести список примеров:</span><span class="sxs-lookup"><span data-stu-id="99d6f-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="99d6f-143">Эта команда создает список примеров из предыдущего раздела данного документа.</span><span class="sxs-lookup"><span data-stu-id="99d6f-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="99d6f-144">Чтобы получить справку по конкретному примеру, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="99d6f-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="99d6f-145">В данном случае запускается пример **wordcount**.</span><span class="sxs-lookup"><span data-stu-id="99d6f-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="99d6f-146">Отобразится следующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="99d6f-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="99d6f-147">Это сообщение означает, что можно указать несколько входных путей для исходных документов.</span><span class="sxs-lookup"><span data-stu-id="99d6f-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="99d6f-148">Окончательный путь — это место, где сохраняются выходные данные (число слов в исходных документах).</span><span class="sxs-lookup"><span data-stu-id="99d6f-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="99d6f-149">Для подсчета всех слов в книге «Записи Леонардо да Винчи», которая поставляется с кластером и служит примером исходных данных, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="99d6f-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="99d6f-150">Для этого задания считываются входные данные из файла `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="99d6f-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="99d6f-151">Выходные данные для этого примера сохраняются в `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="99d6f-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="99d6f-152">Оба пути расположены в хранилище по умолчанию для кластера, а не в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="99d6f-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99d6f-153">Как сказано в справке по примеру wordcount, вы также можете указать несколько входных файлов.</span><span class="sxs-lookup"><span data-stu-id="99d6f-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="99d6f-154">Например, команда `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` позволит подсчитать слова в файлах davinci.txt и ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="99d6f-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="99d6f-155">По завершении задания воспользуйтесь следующей командой, чтобы просмотреть результат:</span><span class="sxs-lookup"><span data-stu-id="99d6f-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="99d6f-156">Эта команда сцепляет все выходные файлы, созданные заданием.</span><span class="sxs-lookup"><span data-stu-id="99d6f-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="99d6f-157">Она отображает выходные данные в консоли.</span><span class="sxs-lookup"><span data-stu-id="99d6f-157">It displays the output to the console.</span></span> <span data-ttu-id="99d6f-158">Результат будет аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="99d6f-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="99d6f-159">Каждая строка соответствует одному слову и частоте его появления в исходных данных.</span><span class="sxs-lookup"><span data-stu-id="99d6f-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="99d6f-160">Пример судоку</span><span class="sxs-lookup"><span data-stu-id="99d6f-160">The Sudoku example</span></span>

<span data-ttu-id="99d6f-161">[Судоку](https://en.wikipedia.org/wiki/Sudoku) — это логическая головоломка, которая состоит из девяти полей размером 3 x 3 клетки.</span><span class="sxs-lookup"><span data-stu-id="99d6f-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="99d6f-162">Некоторые ячейки в клетках содержат числа, остальные ячейки пустые. Задача заключается в поиске чисел для пустых ячеек.</span><span class="sxs-lookup"><span data-stu-id="99d6f-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="99d6f-163">С помощью указанной выше ссылки можно получить дополнительные сведения о головоломке, однако целью этого примера является поиск значений для пустых ячеек.</span><span class="sxs-lookup"><span data-stu-id="99d6f-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="99d6f-164">Таким образом, на входе программы должен быть файл в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="99d6f-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="99d6f-165">Девять строк и девять столбцов</span><span class="sxs-lookup"><span data-stu-id="99d6f-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="99d6f-166">Каждый столбец может содержать число или знак `?` (означает пустую ячейку).</span><span class="sxs-lookup"><span data-stu-id="99d6f-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="99d6f-167">Ячейки разделяются пробелами</span><span class="sxs-lookup"><span data-stu-id="99d6f-167">Cells are separated by a space</span></span>

<span data-ttu-id="99d6f-168">Следующая задача — составление головоломки судоку, по правилам которой не допускается использование одного и того же числа в строке или столбце.</span><span class="sxs-lookup"><span data-stu-id="99d6f-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="99d6f-169">В хранилище кластера HDInsight есть соответствующий пример.</span><span class="sxs-lookup"><span data-stu-id="99d6f-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="99d6f-170">Он находится в `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` и содержит приведенный ниже текст.</span><span class="sxs-lookup"><span data-stu-id="99d6f-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="99d6f-171">Чтобы обработать эти данные в примере судоку, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="99d6f-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="99d6f-172">Полученный текст должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="99d6f-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="99d6f-173">Пример "Пи" (π)</span><span class="sxs-lookup"><span data-stu-id="99d6f-173">Pi (π) example</span></span>

<span data-ttu-id="99d6f-174">В примере «Пи» используется статистический метод (квази-Монте-Карло) оценки значения числа пи.</span><span class="sxs-lookup"><span data-stu-id="99d6f-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="99d6f-175">Точки в произвольном порядке помещаются внутри единичного квадрата.</span><span class="sxs-lookup"><span data-stu-id="99d6f-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="99d6f-176">В квадрат также вписан круг.</span><span class="sxs-lookup"><span data-stu-id="99d6f-176">The square also contains a circle.</span></span> <span data-ttu-id="99d6f-177">Вероятность того, что точки попадут в круг, равна площади круга, π/4.</span><span class="sxs-lookup"><span data-stu-id="99d6f-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="99d6f-178">Значение числа π можно оценить по формуле 4R.</span><span class="sxs-lookup"><span data-stu-id="99d6f-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="99d6f-179">R — это отношение количества точек, находящихся внутри круга, к общему количеству точек, находящихся внутри квадрата.</span><span class="sxs-lookup"><span data-stu-id="99d6f-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="99d6f-180">Чем больше выборка используемых точек, тем точнее оценка.</span><span class="sxs-lookup"><span data-stu-id="99d6f-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="99d6f-181">Для запуска примера используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="99d6f-181">Use the following command to run this sample.</span></span> <span data-ttu-id="99d6f-182">Для оценки числа π в команде используется 16 карт с 10 000 000 примерами в каждой.</span><span class="sxs-lookup"><span data-stu-id="99d6f-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="99d6f-183">Команда должна возвращать значение наподобие **3,14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="99d6f-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="99d6f-184">Для справки, первые 10 знаков числа пи: 3,1415926535.</span><span class="sxs-lookup"><span data-stu-id="99d6f-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="99d6f-185">Пример Greysort для 10 ГБ данных</span><span class="sxs-lookup"><span data-stu-id="99d6f-185">10 GB Greysort example</span></span>

<span data-ttu-id="99d6f-186">GraySort — это измерение производительности сортировки.</span><span class="sxs-lookup"><span data-stu-id="99d6f-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="99d6f-187">Его показателем служит скорость (ТБ/мин), достигаемая при сортировке очень больших объемов данных, обычно не менее 100 ТБ.</span><span class="sxs-lookup"><span data-stu-id="99d6f-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="99d6f-188">В этом примере используется небольшой объем данных, 10 ГБ, чтобы можно было выполнить сортировку достаточно быстро.</span><span class="sxs-lookup"><span data-stu-id="99d6f-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="99d6f-189">Используются приложения MapReduce, разработанные Оуэном О'Мэлли (Owen O'Malley) и Аруном Мёрти (Arun Murthy).</span><span class="sxs-lookup"><span data-stu-id="99d6f-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="99d6f-190">Эти приложения победили в 2009 году на конкурсе приложений сортировки общего назначения (daytona) для больших объемов данных, показав скорость 0,578 ТБ/мин (100 ТБ за 173 минуты).</span><span class="sxs-lookup"><span data-stu-id="99d6f-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="99d6f-191">Дополнительные сведения об этом и других измерениях производительности сортировки см. на веб-сайте [Sortbenchmark](http://sortbenchmark.org/).</span><span class="sxs-lookup"><span data-stu-id="99d6f-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="99d6f-192">В этом примере используются три набора программ MapReduce.</span><span class="sxs-lookup"><span data-stu-id="99d6f-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="99d6f-193">**TeraGen**: программа MapReduce, которая создает строки с данными для последующей сортировки.</span><span class="sxs-lookup"><span data-stu-id="99d6f-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="99d6f-194">**TeraSort**: производит выборку входных данных и использует MapReduce для сортировки данных в общем порядке.</span><span class="sxs-lookup"><span data-stu-id="99d6f-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="99d6f-195">TeraSort представляет собой стандартную сортировку MapReduce, за исключением настраиваемого разделителя.</span><span class="sxs-lookup"><span data-stu-id="99d6f-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="99d6f-196">В разделителе используется отсортированный список выборки ключей N-1, определяющий диапазон ключей для каждой функции reduce.</span><span class="sxs-lookup"><span data-stu-id="99d6f-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="99d6f-197">В частности, все ключи, подобные этому примеру [i-1] <= key < sample[i] отправляются для сокращения i.</span><span class="sxs-lookup"><span data-stu-id="99d6f-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="99d6f-198">Этот разделитель гарантирует, что выходные данные сокращения i будут меньше, чем выходные данные i+1.</span><span class="sxs-lookup"><span data-stu-id="99d6f-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="99d6f-199">**TeraValidate**: программа MapReduce, которая проверяет глобальную сортировку выходных данных.</span><span class="sxs-lookup"><span data-stu-id="99d6f-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="99d6f-200">В выходном каталоге создается одна функция map для каждого файла, и каждая функция map гарантирует, что каждый ключ будет меньше или равен предыдущему.</span><span class="sxs-lookup"><span data-stu-id="99d6f-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="99d6f-201">Функция map создает записи первого и последнего ключей каждого файла.</span><span class="sxs-lookup"><span data-stu-id="99d6f-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="99d6f-202">Функция reduce гарантирует, что первый ключ файла i больше последнего ключа файла i-1.</span><span class="sxs-lookup"><span data-stu-id="99d6f-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="99d6f-203">Все проблемы указываются в выходных данных этапа редукции вместе с неотсортированными ключами.</span><span class="sxs-lookup"><span data-stu-id="99d6f-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="99d6f-204">Для создания данных, сортировки и проверки выходных данных используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="99d6f-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="99d6f-205">Создайте 10 ГБ данных, которые сохранятся в хранилище по умолчанию кластера HDInsight в `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="99d6f-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="99d6f-206">Ключ `-Dmapred.map.tasks` говорит Hadoop о том, сколько задач сопоставления будет использоваться в этом задании.</span><span class="sxs-lookup"><span data-stu-id="99d6f-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="99d6f-207">Последние два параметра означают, что задание создаст 10 ГБ данных и сохранит их в `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="99d6f-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="99d6f-208">Выполните следующую команду, чтобы отсортировать данные:</span><span class="sxs-lookup"><span data-stu-id="99d6f-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="99d6f-209">Ключ `-Dmapred.reduce.tasks` говорит Hadoop о том, сколько задач сокращения будет использоваться в этом задании.</span><span class="sxs-lookup"><span data-stu-id="99d6f-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="99d6f-210">Последние два параметра соответствуют путям расположения входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="99d6f-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="99d6f-211">Используйте следующую команду, чтобы просмотреть отсортированные данные:</span><span class="sxs-lookup"><span data-stu-id="99d6f-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="99d6f-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="99d6f-212">Next steps</span></span>

<span data-ttu-id="99d6f-213">В данной статье рассмотрено выполнение примеров, поставляемых с кластерами HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="99d6f-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="99d6f-214">Учебники по использованию Pig, Hive и MapReduce в службе HDInsight см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="99d6f-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="99d6f-215">[Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="99d6f-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="99d6f-216">[Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="99d6f-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="99d6f-217">[Использование MapReduce в Hadoop в HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="99d6f-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
