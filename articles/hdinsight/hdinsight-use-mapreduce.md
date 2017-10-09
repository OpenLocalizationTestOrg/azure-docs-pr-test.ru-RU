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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>Использование MapReduce в Hadoop в HDInsight

Узнайте, как toorun MapReduce заданий в кластерах HDInsight. Используйте следующие таблицы toodiscover hello различные способы использования MapReduce с HDInsight hello.

| **Используется**... | **.. .toodo это** | ...with этим **кластером операционной системы** | ...из этого **кластера операционной системы** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Команда Hadoop hello через **SSH** |Linux |Linux, Unix, Mac OS X или Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Отправить задание hello удаленно с помощью **REST** (примеры используйте cURL) |Linux или Windows |Linux, Unix, Mac OS X или Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Отправить задание hello удаленно с помощью **Windows PowerShell** |Linux или Windows |Windows |
| [Удаленный рабочий стол](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 и 3.3) |Команда Hadoop hello через **удаленного рабочего стола** |Windows |Windows |

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="whatis"></a>Что такое MapReduce

Hadoop MapReduce — это программная платформа для написания заданий, обрабатывающих большие объемы данных. Входные данные разбивается на независимых блоков, которые затем обрабатываются параллельно через hello узлов в кластере. Задание MapReduce состоит из двух функций.

* **Mapper**(Модуль сопоставления) — принимает входные данные, анализирует их (обычно с помощью фильтрации и сортировки) и передает кортежи (пары «ключ-значение»).

* **Редуктора**: использует кортежей, генерируемой hello сопоставления и выполняет операцию сводки, которая создает результат меньшего размера, вместе с hello сопоставления данных

Пример задания MapReduce для основных word count проиллюстрирован в hello, следующая схема:

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

выходные данные этого задания Hello представляет собой число количество возникновений каждого слова в тексте hello, которое было проанализировано.

* сопоставления Hello принимает каждую строку из входного текста hello, входным и разбивает ее на слова. Он создает ключ значение пары каждый раз встречается слово hello слова следуют 1. Перед отправкой tooreducer отсортирован Hello выход.
* Hello редуктора суммирует этих отдельных счетчиков для каждого слова и создает пару один ключ значение, которая содержит слово hello следуют сумма hello его экземпляров.

Задание MapReduce может быть реализовано на различных языках. Java — наиболее общая реализация hello и используется для демонстрации в этом документе.

## <a name="development-languages"></a>Языки разработки

Непосредственно как задание MapReduce можно выполнялись языков или платформ, которые основаны на Java и hello виртуальной машины Java. пример Hello, используемых в документе представляет собой приложение Java MapReduce. Прочие языки и платформы, например C# или Python, или изолированные исполняемые файлы должны использовать потоковую передачу Hadoop.

Потоковой передачи Hadoop взаимодействует с hello сопоставления и редуктора через STDIN и STDOUT. Hello сопоставления и редуктора считывания строки данных за один раз от STDIN и записи tooSTDOUT hello выходных данных. Каждая строка чтения или испускаемый hello сопоставления и редуктора должен быть в формате hello пары ключ значение, разделенные символом табуляции:

    [key]/t[value]

Дополнительные сведения см. в документации по [потоковой передаче Hadoop](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Примеры использования потоковой передачи с HDInsight Hadoop в разделе hello следующие документы:

* [Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Разработка заданий Python MapReduce](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Демонстрационные данные

HDInsight предоставляет различные пример наборов данных, хранящихся в hello `/example/data` и `/HdiSamples` каталога. Эти каталоги находятся в хранилище по умолчанию hello для кластера. В этом документе мы используем hello `/example/data/gutenberg/davinci.txt` файла. Этот файл содержит записных книжек hello Леонардо да Винчи.

## <a id="job"></a>Пример MapReduce

Пример приложения MapReduce для подсчета слов входит в состав кластера HDInsight. В этом примере расположен в `/example/jars/hadoop-mapreduce-examples.jar` на hello хранилища по умолчанию для кластера.

Следующий пример кода Java Hello является источником hello hello приложения MapReduce, содержащихся в hello `hadoop-mapreduce-examples.jar` файла:

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

Инструкции toowrite собственных приложений MapReduce см hello следующие документы:

* [Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Разработка программ потоковой передачи на Python для HDInsight](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Запустите hello MapReduce

HDInsight может выполнять задания HiveQL, используя различные методы. Используйте следующие таблицы toodecide, какой метод подходит для вас hello, затем по ссылке hello Пошаговое руководство.

| **Используется**... | **.. .toodo это** | ...with этим **кластером операционной системы** | ...из этого **кластера операционной системы** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Команда Hadoop hello через **SSH** |Linux |Linux, Unix, Mac OS X или Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |Отправить задание hello удаленно с помощью **REST** |Linux или Windows |Linux, Unix, Mac OS X или Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Отправить задание hello удаленно с помощью **Windows PowerShell** |Linux или Windows |Windows |
| [Удаленный рабочий стол](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 и 3.3) |Команда Hadoop hello через **удаленного рабочего стола** |Windows |Windows |

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="nextsteps"></a>Дальнейшие действия

toolearn Дополнительные сведения о работе с данными в HDInsight, в разделе hello следующие документы:

* [Разработка программ MapReduce на Java для HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Разработка программ MapReduce с потоковой передачей Python для HDInsight](hdinsight-hadoop-streaming-python.md)

* [Разработка заданий Scalding MapReduce с Apache Hadoop в HDInsight](hdinsight-hadoop-mapreduce-scalding.md)

* [Использование Hive с HDInsight][hdinsight-use-hive]

* [Использование Pig с HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
