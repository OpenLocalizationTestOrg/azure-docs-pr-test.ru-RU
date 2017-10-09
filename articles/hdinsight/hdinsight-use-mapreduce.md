---
title: "aaaMapReduce с Hadoop в HDInsight | Документы Microsoft"
description: "Узнайте, как toorun MapReduce заданий на Hadoop в HDInsight кластеров."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="b1010-103">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1010-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="b1010-104">Узнайте, как toorun MapReduce заданий в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1010-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="b1010-105">Используйте следующие таблицы toodiscover hello различные способы использования MapReduce с HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b1010-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="b1010-106">**Используется**...</span><span class="sxs-lookup"><span data-stu-id="b1010-106">**Use this**...</span></span> | <span data-ttu-id="b1010-107">**.. .toodo это**</span><span class="sxs-lookup"><span data-stu-id="b1010-107">**...toodo this**</span></span> | <span data-ttu-id="b1010-108">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="b1010-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="b1010-109">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="b1010-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="b1010-110">SSH</span><span class="sxs-lookup"><span data-stu-id="b1010-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="b1010-111">Команда Hadoop hello через **SSH**</span><span class="sxs-lookup"><span data-stu-id="b1010-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="b1010-112">Linux</span><span class="sxs-lookup"><span data-stu-id="b1010-112">Linux</span></span> |<span data-ttu-id="b1010-113">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b1010-114">REST</span><span class="sxs-lookup"><span data-stu-id="b1010-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="b1010-115">Отправить задание hello удаленно с помощью **REST** (примеры используйте cURL)</span><span class="sxs-lookup"><span data-stu-id="b1010-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="b1010-116">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-116">Linux or Windows</span></span> |<span data-ttu-id="b1010-117">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b1010-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1010-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="b1010-119">Отправить задание hello удаленно с помощью **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b1010-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="b1010-120">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-120">Linux or Windows</span></span> |<span data-ttu-id="b1010-121">Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-121">Windows</span></span> |
| <span data-ttu-id="b1010-122">[Удаленный рабочий стол](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="b1010-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="b1010-123">Команда Hadoop hello через **удаленного рабочего стола**</span><span class="sxs-lookup"><span data-stu-id="b1010-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="b1010-124">Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-124">Windows</span></span> |<span data-ttu-id="b1010-125">Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="b1010-126">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b1010-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b1010-127">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b1010-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="b1010-128"><a id="whatis"></a>Что такое MapReduce</span><span class="sxs-lookup"><span data-stu-id="b1010-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="b1010-129">Hadoop MapReduce — это программная платформа для написания заданий, обрабатывающих большие объемы данных.</span><span class="sxs-lookup"><span data-stu-id="b1010-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="b1010-130">Входные данные разбивается на независимых блоков, которые затем обрабатываются параллельно через hello узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="b1010-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="b1010-131">Задание MapReduce состоит из двух функций.</span><span class="sxs-lookup"><span data-stu-id="b1010-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="b1010-132">**Mapper**(Модуль сопоставления) — принимает входные данные, анализирует их (обычно с помощью фильтрации и сортировки) и передает кортежи (пары «ключ-значение»).</span><span class="sxs-lookup"><span data-stu-id="b1010-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="b1010-133">**Редуктора**: использует кортежей, генерируемой hello сопоставления и выполняет операцию сводки, которая создает результат меньшего размера, вместе с hello сопоставления данных</span><span class="sxs-lookup"><span data-stu-id="b1010-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="b1010-134">Пример задания MapReduce для основных word count проиллюстрирован в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="b1010-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="b1010-136">выходные данные этого задания Hello представляет собой число количество возникновений каждого слова в тексте hello, которое было проанализировано.</span><span class="sxs-lookup"><span data-stu-id="b1010-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="b1010-137">сопоставления Hello принимает каждую строку из входного текста hello, входным и разбивает ее на слова.</span><span class="sxs-lookup"><span data-stu-id="b1010-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="b1010-138">Он создает ключ значение пары каждый раз встречается слово hello слова следуют 1.</span><span class="sxs-lookup"><span data-stu-id="b1010-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="b1010-139">Перед отправкой tooreducer отсортирован Hello выход.</span><span class="sxs-lookup"><span data-stu-id="b1010-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="b1010-140">Hello редуктора суммирует этих отдельных счетчиков для каждого слова и создает пару один ключ значение, которая содержит слово hello следуют сумма hello его экземпляров.</span><span class="sxs-lookup"><span data-stu-id="b1010-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="b1010-141">Задание MapReduce может быть реализовано на различных языках.</span><span class="sxs-lookup"><span data-stu-id="b1010-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="b1010-142">Java — наиболее общая реализация hello и используется для демонстрации в этом документе.</span><span class="sxs-lookup"><span data-stu-id="b1010-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="b1010-143">Языки разработки</span><span class="sxs-lookup"><span data-stu-id="b1010-143">Development languages</span></span>

<span data-ttu-id="b1010-144">Непосредственно как задание MapReduce можно выполнялись языков или платформ, которые основаны на Java и hello виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="b1010-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="b1010-145">пример Hello, используемых в документе представляет собой приложение Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b1010-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="b1010-146">Прочие языки и платформы, например C# или Python, или изолированные исполняемые файлы должны использовать потоковую передачу Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b1010-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="b1010-147">Потоковой передачи Hadoop взаимодействует с hello сопоставления и редуктора через STDIN и STDOUT.</span><span class="sxs-lookup"><span data-stu-id="b1010-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="b1010-148">Hello сопоставления и редуктора считывания строки данных за один раз от STDIN и записи tooSTDOUT hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b1010-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="b1010-149">Каждая строка чтения или испускаемый hello сопоставления и редуктора должен быть в формате hello пары ключ значение, разделенные символом табуляции:</span><span class="sxs-lookup"><span data-stu-id="b1010-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="b1010-150">Дополнительные сведения см. в документации по [потоковой передаче Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="b1010-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="b1010-151">Примеры использования потоковой передачи с HDInsight Hadoop в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="b1010-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="b1010-152">Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1010-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="b1010-153">Разработка заданий Python MapReduce</span><span class="sxs-lookup"><span data-stu-id="b1010-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="b1010-154"><a id="data"></a>Демонстрационные данные</span><span class="sxs-lookup"><span data-stu-id="b1010-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="b1010-155">HDInsight предоставляет различные пример наборов данных, хранящихся в hello `/example/data` и `/HdiSamples` каталога.</span><span class="sxs-lookup"><span data-stu-id="b1010-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="b1010-156">Эти каталоги находятся в хранилище по умолчанию hello для кластера.</span><span class="sxs-lookup"><span data-stu-id="b1010-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="b1010-157">В этом документе мы используем hello `/example/data/gutenberg/davinci.txt` файла.</span><span class="sxs-lookup"><span data-stu-id="b1010-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="b1010-158">Этот файл содержит записных книжек hello Леонардо да Винчи.</span><span class="sxs-lookup"><span data-stu-id="b1010-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="b1010-159"><a id="job"></a>Пример MapReduce</span><span class="sxs-lookup"><span data-stu-id="b1010-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="b1010-160">Пример приложения MapReduce для подсчета слов входит в состав кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b1010-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="b1010-161">В этом примере расположен в `/example/jars/hadoop-mapreduce-examples.jar` на hello хранилища по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="b1010-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="b1010-162">Следующий пример кода Java Hello является источником hello hello приложения MapReduce, содержащихся в hello `hadoop-mapreduce-examples.jar` файла:</span><span class="sxs-lookup"><span data-stu-id="b1010-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="b1010-163">Инструкции toowrite собственных приложений MapReduce см hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="b1010-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="b1010-164">Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="b1010-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="b1010-165">Разработка программ потоковой передачи на Python для HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1010-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="b1010-166"><a id="run"></a>Запустите hello MapReduce</span><span class="sxs-lookup"><span data-stu-id="b1010-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="b1010-167">HDInsight может выполнять задания HiveQL, используя различные методы.</span><span class="sxs-lookup"><span data-stu-id="b1010-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="b1010-168">Используйте следующие таблицы toodecide, какой метод подходит для вас hello, затем по ссылке hello Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="b1010-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="b1010-169">**Используется**...</span><span class="sxs-lookup"><span data-stu-id="b1010-169">**Use this**...</span></span> | <span data-ttu-id="b1010-170">**.. .toodo это**</span><span class="sxs-lookup"><span data-stu-id="b1010-170">**...toodo this**</span></span> | <span data-ttu-id="b1010-171">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="b1010-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="b1010-172">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="b1010-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="b1010-173">SSH</span><span class="sxs-lookup"><span data-stu-id="b1010-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="b1010-174">Команда Hadoop hello через **SSH**</span><span class="sxs-lookup"><span data-stu-id="b1010-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="b1010-175">Linux</span><span class="sxs-lookup"><span data-stu-id="b1010-175">Linux</span></span> |<span data-ttu-id="b1010-176">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b1010-177">Curl</span><span class="sxs-lookup"><span data-stu-id="b1010-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="b1010-178">Отправить задание hello удаленно с помощью **REST**</span><span class="sxs-lookup"><span data-stu-id="b1010-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="b1010-179">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-179">Linux or Windows</span></span> |<span data-ttu-id="b1010-180">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b1010-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1010-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="b1010-182">Отправить задание hello удаленно с помощью **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b1010-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="b1010-183">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-183">Linux or Windows</span></span> |<span data-ttu-id="b1010-184">Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-184">Windows</span></span> |
| <span data-ttu-id="b1010-185">[Удаленный рабочий стол](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="b1010-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="b1010-186">Команда Hadoop hello через **удаленного рабочего стола**</span><span class="sxs-lookup"><span data-stu-id="b1010-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="b1010-187">Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-187">Windows</span></span> |<span data-ttu-id="b1010-188">Windows</span><span class="sxs-lookup"><span data-stu-id="b1010-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="b1010-189">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b1010-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b1010-190">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b1010-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="b1010-191"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1010-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="b1010-192">toolearn Дополнительные сведения о работе с данными в HDInsight, в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="b1010-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="b1010-193">Разработка программ MapReduce на Java для HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1010-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="b1010-194">Разработка программ MapReduce с потоковой передачей Python для HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1010-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="b1010-195">Разработка заданий Scalding MapReduce с Apache Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b1010-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="b1010-196">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b1010-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="b1010-197">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b1010-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
