---
title: "Примеры aaaRun Hadoop MapReduce в HDInsight - Azure | Документы Microsoft"
description: "Начало работы с образцами MapReduce в файлах JAR, включенных в HDInsight. Использование кластера toohello tooconnect SSH, а затем использовать hello Hadoop команда toorun образец задания."
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
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="6b6b5-105">Запустить примеры hello MapReduce, включенные в HDInsight</span><span class="sxs-lookup"><span data-stu-id="6b6b5-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="6b6b5-106">Узнайте, как включенные примеры MapReduce hello toorun с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b6b5-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6b6b5-107">Prerequisites</span></span>

* <span data-ttu-id="6b6b5-108">**Кластер HDInsight**. См. статью [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6b6b5-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6b6b5-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="6b6b5-111">**SSH-клиент**. Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="6b6b5-112">Примеры MapReduce Hello</span><span class="sxs-lookup"><span data-stu-id="6b6b5-112">hello MapReduce examples</span></span>

<span data-ttu-id="6b6b5-113">**Расположение**: hello образцы расположены на hello в кластер HDInsight `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="6b6b5-114">**Содержимое**: hello следующие образцы находятся в этом архиве:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="6b6b5-115">`aggregatewordcount`: Статистического выражения на основе программу mapreduce, которая подсчитывает слова hello во входных файлах hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="6b6b5-116">`aggregatewordhist`: Статистического выражения на основе программу mapreduce, которая вычисляет гистограмму hello слова hello во входных файлах hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="6b6b5-117">`bbp`: Mapreduce программа, использующая п-в Бейли-Borwein-Plouffe toocompute точные цифры числа пи.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="6b6b5-118">`dbcount`: Задание пример, который подсчитывает hello pageview журналов, хранящихся в базе данных.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="6b6b5-119">`distbbp`: Mapreduce программа, использующая точное bits BBP тип формулы toocompute пи.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="6b6b5-120">`grep`: Mapreduce программу, которая подсчитывает hello соответствует регулярного выражения во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="6b6b5-121">`join`: задание для объединения сортированных наборов данных одного размера.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="6b6b5-122">`multifilewc`: задание для подсчета слов в нескольких файлах.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="6b6b5-123">`pentomino`: Mapreduce плитки размещение программы toofind решения toopentomino проблем.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="6b6b5-124">`pi`: программа MapReduce для расчета числа π по методу квази-Монте-Карло.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="6b6b5-125">`randomtextwriter`: программа MapReduce для записи 10 ГБ случайных текстовых данных на узел.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="6b6b5-126">`randomwriter`: программа MapReduce для записи 10 ГБ случайных данных на узел.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="6b6b5-127">`secondarysort`: Пример определения toohello дополнительной сортировки уменьшить этап.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="6b6b5-128">`sort`: Mapreduce программа, которая сортирует данные hello, записываемых модулем записи случайных hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="6b6b5-129">`sudoku`: программа решения судоку.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="6b6b5-130">`teragen`: Создать данные для hello terasort.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="6b6b5-131">`terasort`: Запустите hello terasort.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="6b6b5-132">`teravalidate`: проверка результатов выполнения программы TeraSort.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="6b6b5-133">`wordcount`: Mapreduce программа, которая подсчитывает слова hello во входных файлах hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="6b6b5-134">`wordmean`: Mapreduce программа, которая подсчитывает hello среднюю длину слова hello во входных файлах hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="6b6b5-135">`wordmedian`: Mapreduce программа, которая подсчитывает hello медианы длина слова hello во входных файлах hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="6b6b5-136">`wordstandarddeviation`: Mapreduce программа, которая подсчитывает стандартное отклонение hello hello длины слова hello во входных файлах hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="6b6b5-137">**Исходный код**: исходный код этих образцов включен в кластер HDInsight на hello `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="6b6b5-138">Hello `2.2.4.9-1` в hello путь — версия hello hello платформы Hortonworks Data Platform для кластера HDInsight hello и может быть разным для кластера.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="6b6b5-139">Выполнить пример счетчика слов hello</span><span class="sxs-lookup"><span data-stu-id="6b6b5-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="6b6b5-140">Подключиться с помощью SSH tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="6b6b5-141">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6b6b5-142">Из hello `username@#######:~$` запрос, используйте следующие примеры hello toolist команд hello:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="6b6b5-143">Эта команда создает список hello образец hello в предыдущем разделе этого документа.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="6b6b5-144">Используйте hello следующая команда tooget справки по определенной выборке.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="6b6b5-145">В этом случае hello **wordcount** образца:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="6b6b5-146">Появляется после сообщения hello:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="6b6b5-147">Это сообщение означает, что вы можете задать несколько путей ввода hello исходные документы.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="6b6b5-148">конечный путь Hello здесь хранятся hello вывода (число слов в документах источника hello).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="6b6b5-149">Используйте следующие toocount hello все слова в hello портативные компьютеры из Леонардо да Винчи, которой будут предоставлены кластера в качестве данных выборки:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="6b6b5-150">Для этого задания считываются входные данные из файла `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="6b6b5-151">Выходные данные для этого примера сохраняются в `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="6b6b5-152">Оба пути находились в хранилище по умолчанию hello кластер, не hello локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6b6b5-153">Как уже отмечалось в справке hello для образца wordcount hello, можно также указать несколько входных файлов.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="6b6b5-154">Например, команда `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` позволит подсчитать слова в файлах davinci.txt и ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="6b6b5-155">После завершения задания hello, используйте следующие выходные данные команды tooview hello hello:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="6b6b5-156">Эта команда объединяет все hello выходные файлы, созданные задания hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="6b6b5-157">Он отображает hello вывода toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-157">It displays hello output toohello console.</span></span> <span data-ttu-id="6b6b5-158">Hello выходных данных аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="6b6b5-159">Каждая строка представляет слова и сколько раз она произошла в hello входные данные.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="6b6b5-160">Пример Судоку Hello</span><span class="sxs-lookup"><span data-stu-id="6b6b5-160">hello Sudoku example</span></span>

<span data-ttu-id="6b6b5-161">[Судоку](https://en.wikipedia.org/wiki/Sudoku) — это логическая головоломка, которая состоит из девяти полей размером 3 x 3 клетки.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="6b6b5-162">Некоторые ячейки в сетке hello есть цифры, тогда как другие пусты, а задача hello — toosolve пустым ячейкам hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="6b6b5-163">предыдущая ссылка Hello содержит дополнительные сведения о головоломки hello, но цель этого образца hello toosolve пустым ячейкам hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="6b6b5-164">Поэтому наши входных данных должен быть файлом в кодировке hello:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="6b6b5-165">Девять строк и девять столбцов</span><span class="sxs-lookup"><span data-stu-id="6b6b5-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="6b6b5-166">Каждый столбец может содержать число или знак `?` (означает пустую ячейку).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="6b6b5-167">Ячейки разделяются пробелами</span><span class="sxs-lookup"><span data-stu-id="6b6b5-167">Cells are separated by a space</span></span>

<span data-ttu-id="6b6b5-168">Нет определенных tooconstruct способом головоломки Судоку; Невозможно повторно число в столбце или строке.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="6b6b5-169">Кластер HDInsight hello, правильно ли построено приводится пример.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="6b6b5-170">Он находится в `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` и содержит hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="6b6b5-171">Используйте эту проблему пример hello примере Судоку toorun hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="6b6b5-172">Hello результаты отображаются как toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="6b6b5-173">Пример "Пи" (π)</span><span class="sxs-lookup"><span data-stu-id="6b6b5-173">Pi (π) example</span></span>

<span data-ttu-id="6b6b5-174">Образец Hello pi использует статистические (реализация Монте Carlo) метод tooestimate hello число пи.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="6b6b5-175">Точки в произвольном порядке помещаются внутри единичного квадрата.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="6b6b5-176">квадрат Hello также содержит круг.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-176">hello square also contains a circle.</span></span> <span data-ttu-id="6b6b5-177">Hello вероятность точек hello подпадающих hello круг, равно toohello области hello circle pi/4.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="6b6b5-178">на основе значения hello 4R можно оценить Hello число пи.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="6b6b5-179">R — отношение hello hello количество точек, которые находятся внутри hello круг toohello общего количества точек, расположенных внутри квадратных hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="6b6b5-180">Hello большего образец hello точек, используемых, является hello лучшую оценку hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="6b6b5-181">Использование этого образца hello, выполнив команду toorun.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="6b6b5-182">Эта команда использует 16 maps с 10 000 000 образцы tooestimate hello число пи:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="6b6b5-183">Hello значение, возвращаемое этой командой аналогично слишком**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="6b6b5-184">Для ссылок hello первые 10 десятичных разрядов числа пи являются 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="6b6b5-185">Пример Greysort для 10 ГБ данных</span><span class="sxs-lookup"><span data-stu-id="6b6b5-185">10 GB Greysort example</span></span>

<span data-ttu-id="6b6b5-186">GraySort — это измерение производительности сортировки.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="6b6b5-187">Hello метрика скорость сортировки hello (ТБ в минуту), достигается при сортировке больших объемов данных, обычно 100 ТБ минимальное.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="6b6b5-188">В этом примере используется небольшой объем данных, 10 ГБ, чтобы можно было выполнить сортировку достаточно быстро.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="6b6b5-189">Она использует hello MapReduce приложения, разработанные с Owen O'Malley и Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="6b6b5-190">Эти приложения hello годовой общего назначения («daytona») терабайт сортировки тестирования выигрыш в 2009 г., с частотой 0.578 ТБ/мин (100 ТБ 173 минут).</span><span class="sxs-lookup"><span data-stu-id="6b6b5-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="6b6b5-191">Дополнительные сведения об этом и других сортировки тестов производительности см. в разделе hello [Sortbenchmark](http://sortbenchmark.org/) сайта.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="6b6b5-192">В этом примере используются три набора программ MapReduce.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="6b6b5-193">**TeraGen**: программу MapReduce, которая приводит к возникновению ряда данных toosort</span><span class="sxs-lookup"><span data-stu-id="6b6b5-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="6b6b5-194">**TeraSort**: образцы hello входных данных и использует данные hello toosort MapReduce в сумма заказа</span><span class="sxs-lookup"><span data-stu-id="6b6b5-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="6b6b5-195">TeraSort представляет собой стандартную сортировку MapReduce, за исключением настраиваемого разделителя.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="6b6b5-196">разделитель Hello использует отсортированный список ключей выборки n-1, определяющие hello диапазона ключей для каждого редукции.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="6b6b5-197">В частности, все ключи такого, образец [i-1] < = ключ < образец [i] отправляются tooreduce я.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="6b6b5-198">Этот разделитель гарантии, что выходные данные hello уменьшить i, меньше, чем выходные данные hello уменьшить i + 1.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="6b6b5-199">**TeraValidate**: глобально сортируется программу MapReduce, которая проверяет hello выходного файла</span><span class="sxs-lookup"><span data-stu-id="6b6b5-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="6b6b5-200">Он создает одно сопоставление каждого файла в выходной каталог hello, и каждая карта гарантирует, что каждый ключ меньше или равно toohello предыдущий.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="6b6b5-201">Функция сопоставления Hello сначала создает записи hello и последний ключи каждого файла.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="6b6b5-202">Hello reduce-функция гарантирует, что hello первый ключ файла i больше, чем последний ключ файла i-1 hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="6b6b5-203">Проблемы выводятся как выход hello уменьшение этапе hello ключей, которые выходят за пределы.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="6b6b5-204">Используйте hello следующие шаги данных toogenerate сортировки, а затем проверять hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="6b6b5-205">Создать 10 ГБ данных, которая является хранилищем по умолчанию кластер HDInsight хранимых toohello на `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="6b6b5-206">Hello `-Dmapred.map.tasks` сообщает, сколько toouse карты задач для этого задания Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="6b6b5-207">Hello две последних параметра означают, что задание toocreate hello 10 ГБ данных и toostore его в параметре `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="6b6b5-208">Используйте следующие команды toosort hello данные hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="6b6b5-209">Hello `-Dmapred.reduce.tasks` Hadoop сообщает, сколько уменьшить toouse задачи для задания hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="6b6b5-210">Параметры Hello две последних просто hello ввода и вывода ячейки данных.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="6b6b5-211">Используйте следующие созданные hello сортировать данные hello toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="6b6b5-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b6b5-212">Next steps</span></span>

<span data-ttu-id="6b6b5-213">Из этой статьи вы узнали, как образцы hello toorun входящий в состав hello кластеры HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="6b6b5-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="6b6b5-214">Руководства об использовании с HDInsight Pig, Hive и MapReduce см hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6b6b5-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="6b6b5-215">[Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6b6b5-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="6b6b5-216">[Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6b6b5-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="6b6b5-217">[Использование MapReduce в Hadoop в HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6b6b5-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
