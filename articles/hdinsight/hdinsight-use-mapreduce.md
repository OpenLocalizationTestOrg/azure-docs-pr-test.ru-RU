---
title: "MapReduce с Hadoop в HDInsight | Документация Майкрософт"
description: "Узнайте, как запускать задания MapReduce в Hadoop в кластере HDInsight."
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="81538-103">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="81538-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="81538-104">Узнайте, как выполнять задания MapReduce в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81538-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="81538-105">Воспользуйтесь приведенной таблицей, чтобы узнать, как можно использовать MapReduce с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81538-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="81538-106">**Используется**...</span><span class="sxs-lookup"><span data-stu-id="81538-106">**Use this**...</span></span> | <span data-ttu-id="81538-107">**... чтобы сделать**</span><span class="sxs-lookup"><span data-stu-id="81538-107">**...to do this**</span></span> | <span data-ttu-id="81538-108">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="81538-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="81538-109">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="81538-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="81538-110">SSH</span><span class="sxs-lookup"><span data-stu-id="81538-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="81538-111">Использование команды Hadoop через **SSH**</span><span class="sxs-lookup"><span data-stu-id="81538-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="81538-112">Linux</span><span class="sxs-lookup"><span data-stu-id="81538-112">Linux</span></span> |<span data-ttu-id="81538-113">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="81538-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="81538-114">REST</span><span class="sxs-lookup"><span data-stu-id="81538-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="81538-115">Удаленная отправка задания с помощью **REST** (в примерах используется cURL)</span><span class="sxs-lookup"><span data-stu-id="81538-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="81538-116">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="81538-116">Linux or Windows</span></span> |<span data-ttu-id="81538-117">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="81538-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="81538-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="81538-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="81538-119">Удаленная отправка заданий с помощью **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="81538-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="81538-120">Windows или Linux</span><span class="sxs-lookup"><span data-stu-id="81538-120">Linux or Windows</span></span> |<span data-ttu-id="81538-121">Windows</span><span class="sxs-lookup"><span data-stu-id="81538-121">Windows</span></span> |
| <span data-ttu-id="81538-122">[Удаленный рабочий стол](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="81538-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="81538-123">Использование команды Hadoop с помощью **удаленного рабочего стола**</span><span class="sxs-lookup"><span data-stu-id="81538-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="81538-124">Windows</span><span class="sxs-lookup"><span data-stu-id="81538-124">Windows</span></span> |<span data-ttu-id="81538-125">Windows</span><span class="sxs-lookup"><span data-stu-id="81538-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="81538-126">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="81538-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="81538-127">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="81538-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="81538-128"><a id="whatis"></a>Что такое MapReduce</span><span class="sxs-lookup"><span data-stu-id="81538-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="81538-129">Hadoop MapReduce — это программная платформа для написания заданий, обрабатывающих большие объемы данных.</span><span class="sxs-lookup"><span data-stu-id="81538-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="81538-130">Входные данные разбиваются на независимые блоки, которые затем обрабатываются параллельно на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="81538-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="81538-131">Задание MapReduce состоит из двух функций.</span><span class="sxs-lookup"><span data-stu-id="81538-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="81538-132">**Mapper**(Модуль сопоставления) — принимает входные данные, анализирует их (обычно с помощью фильтрации и сортировки) и передает кортежи (пары «ключ-значение»).</span><span class="sxs-lookup"><span data-stu-id="81538-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="81538-133">**Reducer**(Редуктор) — принимает кортежи, сформированные в модуле сопоставления, и выполняет операцию сводки, которая создает результат меньшего размера, объединяющий данные модуля сопоставления</span><span class="sxs-lookup"><span data-stu-id="81538-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="81538-134">На следующей диаграмме показан пример задания MapReduce, которое выполняет простую операцию подсчета слов:</span><span class="sxs-lookup"><span data-stu-id="81538-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="81538-136">Выходные данные этого задания представляют собой частоту использования каждого слова в тексте, который был проанализирован.</span><span class="sxs-lookup"><span data-stu-id="81538-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="81538-137">Процедура map берет каждую строку из входного текста в качестве входных данных и разбивает ее на слова.</span><span class="sxs-lookup"><span data-stu-id="81538-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="81538-138">Она генерирует пару «ключ-значение» каждый раз, когда встречается слово, за которым следует 1.</span><span class="sxs-lookup"><span data-stu-id="81538-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="81538-139">Перед отправкой на обработку редуктором выходные данные сортируются.</span><span class="sxs-lookup"><span data-stu-id="81538-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="81538-140">Затем редуктор суммирует эти отдельные счетчики для каждого слова и выдает одну пару «ключ-значение», содержащую слово, за которым следует частота его использования.</span><span class="sxs-lookup"><span data-stu-id="81538-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="81538-141">Задание MapReduce может быть реализовано на различных языках.</span><span class="sxs-lookup"><span data-stu-id="81538-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="81538-142">Java — это наиболее распространенная реализация, которая используется в данном документе для примера.</span><span class="sxs-lookup"><span data-stu-id="81538-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="81538-143">Языки разработки</span><span class="sxs-lookup"><span data-stu-id="81538-143">Development languages</span></span>

<span data-ttu-id="81538-144">Языки или платформы на основе Java или виртуальной машины Java можно запускать непосредственно как задание MapReduce.</span><span class="sxs-lookup"><span data-stu-id="81538-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="81538-145">В качестве примера в этом документе приведено приложение MapReduce на языке Java.</span><span class="sxs-lookup"><span data-stu-id="81538-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="81538-146">Прочие языки и платформы, например C# или Python, или изолированные исполняемые файлы должны использовать потоковую передачу Hadoop.</span><span class="sxs-lookup"><span data-stu-id="81538-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="81538-147">Потоковая передача Hadoop взаимодействует с модулями сопоставления и редукции через потоки STDIN и STDOUT.</span><span class="sxs-lookup"><span data-stu-id="81538-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="81538-148">Модули сопоставления и редукции построчно считывают данные из потока STDIN и записывают выходные данные в поток STDOUT.</span><span class="sxs-lookup"><span data-stu-id="81538-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="81538-149">Каждая строка, которая читается или генерируется модулем сопоставления или редукции, должна быть в формате пар "ключ-значение", разделенных знаком табуляции.</span><span class="sxs-lookup"><span data-stu-id="81538-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="81538-150">Дополнительные сведения см. в документации по [потоковой передаче Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="81538-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="81538-151">Примеры использования потоковой передачи Hadoop с HDInsight приведены в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="81538-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="81538-152">Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="81538-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="81538-153">Разработка заданий Python MapReduce</span><span class="sxs-lookup"><span data-stu-id="81538-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="81538-154"><a id="data"></a>Демонстрационные данные</span><span class="sxs-lookup"><span data-stu-id="81538-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="81538-155">HDInsight предоставляет различные наборы демонстрационных данных, которые хранятся в каталогах `/example/data` и `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="81538-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="81538-156">Эти каталоги находятся в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="81538-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="81538-157">В этом документе мы используем файл `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="81538-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="81538-158">Этот файл содержит записные книжки Леонардо да Винчи.</span><span class="sxs-lookup"><span data-stu-id="81538-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="81538-159"><a id="job"></a>Пример MapReduce</span><span class="sxs-lookup"><span data-stu-id="81538-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="81538-160">Пример приложения MapReduce для подсчета слов входит в состав кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81538-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="81538-161">Этот примере расположен в каталоге `/example/jars/hadoop-mapreduce-examples.jar` в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="81538-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="81538-162">Ниже приведен исходный код Java приложения MapReduce из файла `hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="81538-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="81538-163">Инструкции по написанию приложений MapReduce см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="81538-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="81538-164">Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="81538-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="81538-165">Разработка программ потоковой передачи на Python для HDInsight</span><span class="sxs-lookup"><span data-stu-id="81538-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="81538-166"><a id="run"></a>Запуск MapReduce</span><span class="sxs-lookup"><span data-stu-id="81538-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="81538-167">HDInsight может выполнять задания HiveQL, используя различные методы.</span><span class="sxs-lookup"><span data-stu-id="81538-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="81538-168">Используйте следующую таблицу, чтобы решить, какой метод подходит вам, а затем перейдите по ссылке к пошаговому руководству.</span><span class="sxs-lookup"><span data-stu-id="81538-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="81538-169">**Используется**...</span><span class="sxs-lookup"><span data-stu-id="81538-169">**Use this**...</span></span> | <span data-ttu-id="81538-170">**... чтобы сделать**</span><span class="sxs-lookup"><span data-stu-id="81538-170">**...to do this**</span></span> | <span data-ttu-id="81538-171">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="81538-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="81538-172">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="81538-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="81538-173">SSH</span><span class="sxs-lookup"><span data-stu-id="81538-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="81538-174">Использование команды Hadoop через **SSH**</span><span class="sxs-lookup"><span data-stu-id="81538-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="81538-175">Linux</span><span class="sxs-lookup"><span data-stu-id="81538-175">Linux</span></span> |<span data-ttu-id="81538-176">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="81538-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="81538-177">Curl</span><span class="sxs-lookup"><span data-stu-id="81538-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="81538-178">Удаленная отправка заданий с помощью **REST**</span><span class="sxs-lookup"><span data-stu-id="81538-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="81538-179">Windows или Linux</span><span class="sxs-lookup"><span data-stu-id="81538-179">Linux or Windows</span></span> |<span data-ttu-id="81538-180">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="81538-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="81538-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="81538-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="81538-182">Удаленная отправка заданий с помощью **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="81538-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="81538-183">Windows или Linux</span><span class="sxs-lookup"><span data-stu-id="81538-183">Linux or Windows</span></span> |<span data-ttu-id="81538-184">Windows</span><span class="sxs-lookup"><span data-stu-id="81538-184">Windows</span></span> |
| <span data-ttu-id="81538-185">[Удаленный рабочий стол](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="81538-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="81538-186">Использование команды Hadoop с помощью **удаленного рабочего стола**</span><span class="sxs-lookup"><span data-stu-id="81538-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="81538-187">Windows</span><span class="sxs-lookup"><span data-stu-id="81538-187">Windows</span></span> |<span data-ttu-id="81538-188">Windows</span><span class="sxs-lookup"><span data-stu-id="81538-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="81538-189">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="81538-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="81538-190">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="81538-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="81538-191"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81538-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="81538-192">Чтобы узнать больше о работе с данными в HDInsight, ознакомьтесь со следующими документами:</span><span class="sxs-lookup"><span data-stu-id="81538-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="81538-193">Разработка программ MapReduce на Java для HDInsight</span><span class="sxs-lookup"><span data-stu-id="81538-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="81538-194">Разработка программ MapReduce с потоковой передачей Python для HDInsight</span><span class="sxs-lookup"><span data-stu-id="81538-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="81538-195">Разработка заданий Scalding MapReduce с Apache Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="81538-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="81538-196">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="81538-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="81538-197">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="81538-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
