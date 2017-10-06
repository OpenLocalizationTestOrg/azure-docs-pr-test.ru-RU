---
title: "образцы aaaRun hello Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Начало использования службы Azure HDInsight hello с предоставленными образцами hello. Использование сценариев PowerShell, которые запускают программы MapReduce в кластерах данных."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Выполнение примеров Hadoop MapReduce в HDInsight на базе Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Набор образцов предоставляются toohelp, можно приступить к выполнению задания MapReduce в кластерах Hadoop с использованием Azure HDInsight. Эти образцы доступны на каждом из hello HDInsight управляемого кластеры, создаваемые. Выполнение этих образцов ознакомления с помощью задания toorun командлетов Azure PowerShell для кластеров Hadoop.

* [**Счетчик слов**][hdinsight-sample-wordcount]: подсчитывает количество вхождений слова в текстовом файле.
* [**Потоковая передача количество слов в C#**][hdinsight-sample-csharp-streaming]: количества вхождений слова в текстовом файле с помощью hello интерфейс потоковой передачи Hadoop.
* [**Оценщик pi**][hdinsight-sample-pi-estimator]: использует статистические (реализация Монте Carlo) метод tooestimate hello число пи.
* [**Сортировка данных объемом 10 ГБ (Graysort)**][hdinsight-sample-10gb-graysort]: демонстрирует выполнение универсальной сортировки GraySort для файла размером 10 ГБ с помощью HDInsight. Существует три задания toorun: hello Teragen toogenerate данных, данные hello toosort Terasort и tooconfirm Teravalidate должным образом отсортированы данные hello.

> [!NOTE]
> Hello исходного кода можно найти в приложение hello.

Существует намного дополнительная документация по веб-сайта hello технологий, связанные с Hadoop, таких как программирование на языке Java MapReduce и потоковой передачи и документацию о командлетах, использованных в Windows PowerShell для hello сценариев. Дополнительную информацию об этих файлах см. в следующих разделах.

* [Разработка программ MapReduce на Java для Hadoop в HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Введение tooAzure HDInsight][hdinsight-introduction]

В настоящее время многие делают выбор в пользу Hive и Pig, а не MapReduce.  Дополнительные сведения можно найти в разделе 

* [Использование Hive в HDInsight](hdinsight-use-hive.md)
* [Использование Pig в HDInsight](hdinsight-use-pig.md)

**Предварительные требования**:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Кластер HDInsight**. Инструкции hello различными способами, в которых могут создаваться таких кластеров см. в разделе [кластеров создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Рабочая станция с Azure PowerShell**.

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.
    >
    > Следуйте указаниям hello [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell. При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Статистика — Java
toosubmit проекта MapReduce, сначала создать определение задания MapReduce. В определении задания hello, необходимо указать jar-файл программы MapReduce hello и расположение hello hello jar файла, который является **wasb:///example/jars/hadoop-mapreduce-examples.jar**hello имя класса и аргументы hello.  программу MapReduce wordcount Hello принимает два аргумента: hello исходного файла, который используется toocount слов и место hello выходных данных.

Hello исходного кода можно найти в hello [приложение A](#apendix-a---the-word-count-MapReduce-program-in-java).

Процедура hello разработки Java MapReduce программы см. в разделе - [программ MapReduce разработка Java для Hadoop в HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

**toosubmit задание MapReduce число слов**

1. Откройте **интегрированную среду сценариев Windows PowerShell**. Инструкции по установке и настройке Azure PowerShell см. в статье [Установка и настройка служб Azure PowerShell][powershell-install-configure].
2. Вставьте следующий сценарий PowerShell hello:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    Hello задания MapReduce создает файл с именем *часть r-00000*, который содержит слова, и подсчитывает hello. Hello скрипт использует hello **findstr** toolist hello все слова, команда содержит *«there»*.
3. Первые три переменные задать hello и запустите сценарий hello.

## <a name="hdinsight-sample-csharp-streaming"></a>Статистика — потоковая передача на C#
Hadoop предоставляет tooMapReduce API потоковой передачи, что позволяет toowrite карты и уменьшить функциям в языках, отличных от Java.

> [!NOTE]
> Hello действия в этом учебнике применимы только на основе tooWindows кластеров HDInsight. Пример потоковой передачи для кластеров HDInsight под управлением Linux см. в статье [Разработка программ потоковой передачи на Python для HDInsight](hdinsight-hadoop-streaming-python.md).

В примере hello hello сопоставления и редуктора hello, исполняемые файлы, которые считывают hello входные данные из [stdin] [ stdin-stdout-stderr] (строка за строкой) и вывести результаты hello слишком[stdout] [stdin-stdout-stderr]. Программа Hello подсчитывает все слова hello в тексте hello.

При указании исполняемый файл для **модули сопоставления**, каждая задача сопоставления запускает исполняемый файл как отдельный процесс hello при инициализации модуля сопоставления hello. Запускает задачу hello сопоставления, он преобразует его входные данные в строках и веб-каналы hello toohello строки [stdin] [ stdin-stdout-stderr] процесса hello.

В hello временем сопоставления hello сбор hello строк вывода stdout hello hello процесса. Он преобразует каждую строку в пара ключ значение, в которой собирается hello выходные данные сопоставления hello. По умолчанию hello префикс строку вверх toohello первый символ табуляции является ключом hello и hello остаток строки hello (за исключением hello символ табуляции) значение hello. Если строка hello не символ табуляции, вся строка будет рассматриваться как ключ hello и hello значение равно null.

При указании исполняемый файл для **reducers**, каждая задача редуктора запускает исполняемый файл как отдельный процесс hello при инициализации hello редуктора. Запускает задачу редуктора hello, преобразует его пары ввода ключа и значения в строки и веб-каналы toohello строки hello [stdin] [ stdin-stdout-stderr] процесса hello.

В hello временем редуктора hello собирает hello строк вывода от hello [stdout] [ stdin-stdout-stderr] процесса hello. Он преобразует каждая пара ключ значение tooa строки, которой собираются в качестве выходных данных hello hello редуктора. По умолчанию hello префикс строку вверх toohello первый символ табуляции является ключом hello и hello остаток строки hello (за исключением hello символ табуляции) значение hello.

**Задание числа word потоковой передачи toosubmit C#**

* Выполните процедуру hello в [число - Java слов](#word-count-java)и замените определение задания hello hello, следующей строкой:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    должны быть Hello выходной файл:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>Оценка числа пи
Оценщик pi Hello использует статистические (реализация Монте Carlo) метод tooestimate hello число пи. Точки помещении в произвольном порядке в единое квадратная также попадают в круг с областью равно toohello вероятность круга hello в новом внутри этого квадрата pi/4. на основе значения hello 4R, где R — отношение hello hello количество точек, которые находятся внутри hello круг toohello общего количества точек, расположенных внутри квадратных hello можно оценить Hello число пи. Hello большего образец hello точек, используемых, является hello лучшую оценку hello.

Hello скрипт, предоставленный для данного образца отправляет задание Hadoop jar и настроены toorun со значением 16 карты, каждый из которых является toocompute требуется 10 миллионов точках образец hello значения параметров. Параметр, эти значения могут быть изменены tooimprove hello предполагаемое число пи. Справочник по hello первые 10 десятичных разрядов числа пи являются 3.1415926535.

**toosubmit задание оценки pi**

* Выполните процедуру hello в [число - Java слов](#word-count-java)и замените определение задания hello hello, следующей строкой:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>Сортировка Graysort 10 ГБ
В этом примере используется небольшой объем данных, 10 ГБ, чтобы можно было выполнить сортировку достаточно быстро. Она использует hello MapReduce приложения, разработанные с Owen O'Malley и Arun Murthy, выиграл hello годовой общего назначения («daytona») терабайт сортировки теста производительности в 2009 г. с частотой ТБ 0.578/мин (100 ТБ 173 минут). Дополнительные сведения об этом и других сортировки тестов производительности см. в разделе hello [Sortbenchmark](http://sortbenchmark.org/) сайта.

В этом примере используются три набора программ MapReduce.

1. **TeraGen** представляет собой программу MapReduce, которые можно использовать строки hello toogenerate toosort данных.
2. **TeraSort** выборку hello входных данных и использует данные hello toosort MapReduce в общий порядок. TeraSort представляет собой стандартный MapReduce функции, за исключением пользовательского модуля разделения, использующий отсортированный список ключей выборки n-1, определяющие hello диапазона ключей для каждого редукции. В частности, все ключи такого, образец [i-1] < = ключ < образец [i] отправляются tooreduce я. Это гарантирует, что выходные данные hello уменьшить i, меньше, чем выходные данные hello уменьшить i + 1.
3. **TeraValidate** является глобально сортируется программу MapReduce, которая проверяет hello выходного файла. Он создает одно сопоставление каждого файла в выходной каталог hello, и каждая карта гарантирует, что каждый ключ меньше или равно toohello предыдущий. Функция сопоставления Hello также приводит к возникновению ошибки записи hello сначала и последний разделы для каждого файла и hello reduce-функция гарантирует, что hello первый ключ файла i больше, чем последний ключ файла i-1 hello. Сообщено обо всех проблемах как выходные данные hello уменьшить hello ключей, которые выходят за пределы.

Hello входной и выходной формат, используемый все три приложения считывают и записывают hello текстовых файлов в правильный формат hello. выходные данные Hello hello уменьшить репликации задал too1, а не по умолчанию hello 3, поскольку проверкой hello тестирования производительности не требуется, hello выходные данные реплицировались на узлах toomultiple.

В образце hello, каждого соответствующего tooone hello программ MapReduce, описанные в введение hello необходимо выполнить три задачи.

1. Создать hello данные для сортировки, запустив hello **TeraGen** задания MapReduce.
2. Сортировка данных hello, запустив hello **TeraSort** задания MapReduce.
3. Убедитесь, правильно отсортированы данные hello, запустив hello **TeraValidate** задания MapReduce.

**toosubmit hello заданий**

* Выполните процедуру hello в [число - Java слов](#word-count-java), и используйте hello после определения заданий:

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Дальнейшие действия
Из этой статьи и статьи hello в каждом из примеров hello вы узнали, как образцы hello toorun состава hello кластеров HDInsight с помощью Azure PowerShell. Руководства об использовании с HDInsight Pig, Hive и MapReduce см hello следующие вопросы:

* [Начало работы с Hadoop Hive используется мобильного телефона tooanalyze HDInsight][hdinsight-get-started]
* [Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]
* [Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]
* [Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]
* [Документация по пакету SDK для Azure HDInsight][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Приложение А hello Word count исходного кода.

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Приложение Б. Статистика hello потоковой передачи исходного кода.
Hello MapReduce программой hello cat.exe как текст hello toostream сопоставление интерфейса в консоль hello и hello wc.exe приложениями как hello уменьшение интерфейс toocount hello число слов, которые передаются потоком из документа. Hello сопоставления и редуктора считывание символов, строка за строкой, из стандартного входного потока hello (stdin) и записи toohello стандартного потока вывода (stdout).

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Здравствуйте сопоставления кода в файл использует hello cat.cs [StreamReader] [ streamreader] объекта символов hello tooread hello входящего потока toohello консоли Здравствуйте поток toohello стандартный выходной поток, который затем производит запись с помощью статических hello [Console.Writeline] [ console-writeline] метод.

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Здравствуйте редуктора кода в файл использует hello wc.cs [StreamReader] [ streamreader] объекта tooread символов из hello стандартный входной поток, были, получаемый в результате сопоставления cat.exe hello. При чтении символов hello с hello [Console.Writeline] [ console-writeline] метод, он считает слова hello путем подсчета пробелы и символы конца строки в конце каждого слова в hello. Затем он записывает hello общее toohello стандартный выходной поток с hello [Console.Writeline] [ console-writeline] метод.

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Приложение В hello Pi оценки исходного кода.
Оценщик pi Hello код Java, содержащий сопоставления и редуктора функции hello доступен для проверки ниже. Программа Hello сопоставления создает указанное число точек в произвольном порядке размещена внутри единичного квадрата и затем подсчитывает число hello те точки, где находятся внутри круг hello. Программа редуктора Hello накапливает точки учитываются hello модули сопоставления и затем оценивает hello число пи из формул 4R hello, где R — отношение hello hello количество точек, учитываются внутри hello круг toohello общего количества точек, расположенных внутри квадратных hello.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Приложение D - hello 10 ГБ graysort исходного кода
для изучения этого раздела представлены кода Hello для программы TeraSort MapReduce hello.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
