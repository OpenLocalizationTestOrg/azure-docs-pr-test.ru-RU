---
title: "Использование Hadoop Pig в HDInsight | Документация Майкрософт"
description: "Научитесь использовать Pig с Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="1e7c4-103">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e7c4-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="1e7c4-104">Узнайте, как использовать [Apache Pig](http://pig.apache.org/) с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="1e7c4-105">Pig — это платформа, позволяющая создавать программы для Hadoop с помощью процедурного языка, известного как *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="1e7c4-106">Pig, который является альтернативой Java для создания решений *MapReduce* , входит в состав Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="1e7c4-107">Воспользуйтесь приведенной таблицей, чтобы узнать, как можно использовать Pig с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="1e7c4-108">**Используйте** , если требуется...</span><span class="sxs-lookup"><span data-stu-id="1e7c4-108">**Use this** if you want...</span></span> | <span data-ttu-id="1e7c4-109">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="1e7c4-109">...an **interactive** shell</span></span> | <span data-ttu-id="1e7c4-110">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="1e7c4-110">...**batch** processing</span></span> | <span data-ttu-id="1e7c4-111">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="1e7c4-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="1e7c4-112">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="1e7c4-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="1e7c4-113">SSH</span><span class="sxs-lookup"><span data-stu-id="1e7c4-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="1e7c4-114">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-114">✔</span></span> |<span data-ttu-id="1e7c4-115">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-115">✔</span></span> |<span data-ttu-id="1e7c4-116">Linux</span><span class="sxs-lookup"><span data-stu-id="1e7c4-116">Linux</span></span> |<span data-ttu-id="1e7c4-117">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1e7c4-118">REST API</span><span class="sxs-lookup"><span data-stu-id="1e7c4-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="1e7c4-119">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-119">✔</span></span> |<span data-ttu-id="1e7c4-120">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-120">Linux or Windows</span></span> |<span data-ttu-id="1e7c4-121">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1e7c4-122">.NET SDK для Hadoop</span><span class="sxs-lookup"><span data-stu-id="1e7c4-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="1e7c4-123">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-123">✔</span></span> |<span data-ttu-id="1e7c4-124">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-124">Linux or Windows</span></span> |<span data-ttu-id="1e7c4-125">Windows (сейчас)</span><span class="sxs-lookup"><span data-stu-id="1e7c4-125">Windows (for now)</span></span> |
| [<span data-ttu-id="1e7c4-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e7c4-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="1e7c4-127">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-127">✔</span></span> |<span data-ttu-id="1e7c4-128">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-128">Linux or Windows</span></span> |<span data-ttu-id="1e7c4-129">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-129">Windows</span></span> |
| <span data-ttu-id="1e7c4-130">[Удаленный рабочий стол](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="1e7c4-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="1e7c4-131">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-131">✔</span></span> |<span data-ttu-id="1e7c4-132">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-132">✔</span></span> |<span data-ttu-id="1e7c4-133">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-133">Windows</span></span> |<span data-ttu-id="1e7c4-134">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1e7c4-135">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1e7c4-136">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1e7c4-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="1e7c4-137"><a id="why"></a>Почему именно Pig?</span><span class="sxs-lookup"><span data-stu-id="1e7c4-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="1e7c4-138">Одна из трудностей обработки данных с помощью MapReduce в Hadoop заключается в реализации логики обработки с использованием только функций map и reduce.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="1e7c4-139">Для сложных задач часто приходится разбивать обработку на несколько операций MapReduce, соединенных друг с другом, чтобы достичь желаемого результата.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="1e7c4-140">Pig позволяет определить обработку как ряд преобразований, через которые проходят данные для получения желаемого результата.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="1e7c4-141">Язык Pig Latin позволяет описывать поток данных так, чтобы из необработанных входных данных можно было получить нужный результата посредством одного или нескольких преобразований.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="1e7c4-142">Программы Pig Latin следуют общему шаблону:</span><span class="sxs-lookup"><span data-stu-id="1e7c4-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="1e7c4-143">**Загрузка**: чтение данных для обработки из файловой системы.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="1e7c4-144">**Преобразование**: обработка данных.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="1e7c4-145">**Дамп или сохранение**: вывод данных на экран или сохранение их для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="1e7c4-146">Определяемые пользователем функции</span><span class="sxs-lookup"><span data-stu-id="1e7c4-146">User-defined functions</span></span>

<span data-ttu-id="1e7c4-147">Pig Latin также поддерживает пользовательские функции, позволяющие вызывать внешние компоненты, реализующие логику, которую трудно смоделировать в Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="1e7c4-148">Дополнительные сведения о Pig Latin см. в [справочном руководстве по Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) и [справочном руководстве по Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="1e7c4-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="1e7c4-149">Примеры использования пользовательских функций в Hive см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="1e7c4-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="1e7c4-150">[Использование DataFu с Pig в HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) — DataFu представляет собой коллекцию полезных определяемых пользователем функций, поддерживаемых Apache</span><span class="sxs-lookup"><span data-stu-id="1e7c4-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="1e7c4-151">Использование Python с Pig и Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e7c4-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="1e7c4-152">Использование C# с Hive и Pig в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e7c4-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="1e7c4-153"><a id="data"></a>Демонстрационные данные</span><span class="sxs-lookup"><span data-stu-id="1e7c4-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="1e7c4-154">HDInsight предоставляет различные наборы демонстрационных данных, которые хранятся в каталогах `/example/data` и `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="1e7c4-155">Эти каталоги находятся в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="1e7c4-156">В примере Pig в этом документе используется файл *log4j* из `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="1e7c4-157">Каждый журнал в файле состоит из строки полей, содержащей поле `[LOG LEVEL]` для отображения типа и серьезности.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="1e7c4-158">В предыдущем примере уровень журнала имеет значение ERROR ("ошибка").</span><span class="sxs-lookup"><span data-stu-id="1e7c4-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="1e7c4-159">Вы также можете создать файл log4j с помощью средства ведения журнала [Apache Log4j](http://en.wikipedia.org/wiki/Log4j), а затем отправить этот файл в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="1e7c4-160">Дополнительные сведения см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1e7c4-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="1e7c4-161">Дополнительные сведения о том, каким образом большие двоичные объекты в службе хранилища Azure используются с HDInsight, см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1e7c4-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="1e7c4-162"><a id="job"></a>Пример задания</span><span class="sxs-lookup"><span data-stu-id="1e7c4-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="1e7c4-163">Следующее задание Pig Latin загружает файл `sample.log` из хранилища по умолчанию для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="1e7c4-164">Затем оно выполняет ряд преобразований, которые позволяют подсчитать, сколько раз каждый из уровней ведения журнала был указан во входных данных.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="1e7c4-165">Результаты записываются в поток STDOUT.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="1e7c4-166">На следующем рисунке показано, что каждое из преобразований делает с данным.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-166">The following image shows a summary of what each transformation does to the data.</span></span>

![Графическое представление преобразований][image-hdi-pig-data-transformation]

## <span data-ttu-id="1e7c4-168"><a id="run"></a>Запуск задания Pig Latin</span><span class="sxs-lookup"><span data-stu-id="1e7c4-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="1e7c4-169">HDInsight может запускать задания Pig Latin с помощью различных методов.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="1e7c4-170">Используйте следующую таблицу, чтобы решить, какой метод подходит вам, а затем перейдите по ссылке, чтобы открыть пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="1e7c4-171">**Используйте** , если требуется...</span><span class="sxs-lookup"><span data-stu-id="1e7c4-171">**Use this** if you want...</span></span> | <span data-ttu-id="1e7c4-172">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="1e7c4-172">...an **interactive** shell</span></span> | <span data-ttu-id="1e7c4-173">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="1e7c4-173">...**batch** processing</span></span> | <span data-ttu-id="1e7c4-174">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="1e7c4-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="1e7c4-175">… в этом **клиенте**</span><span class="sxs-lookup"><span data-stu-id="1e7c4-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="1e7c4-176">SSH</span><span class="sxs-lookup"><span data-stu-id="1e7c4-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="1e7c4-177">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-177">✔</span></span> |<span data-ttu-id="1e7c4-178">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-178">✔</span></span> |<span data-ttu-id="1e7c4-179">Linux</span><span class="sxs-lookup"><span data-stu-id="1e7c4-179">Linux</span></span> |<span data-ttu-id="1e7c4-180">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1e7c4-181">Curl</span><span class="sxs-lookup"><span data-stu-id="1e7c4-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="1e7c4-182">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-182">✔</span></span> |<span data-ttu-id="1e7c4-183">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-183">Linux or Windows</span></span> |<span data-ttu-id="1e7c4-184">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1e7c4-185">.NET SDK для Hadoop</span><span class="sxs-lookup"><span data-stu-id="1e7c4-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="1e7c4-186">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-186">✔</span></span> |<span data-ttu-id="1e7c4-187">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-187">Linux or Windows</span></span> |<span data-ttu-id="1e7c4-188">Windows (сейчас)</span><span class="sxs-lookup"><span data-stu-id="1e7c4-188">Windows (for now)</span></span> |
| [<span data-ttu-id="1e7c4-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e7c4-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="1e7c4-190">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-190">✔</span></span> |<span data-ttu-id="1e7c4-191">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-191">Linux or Windows</span></span> |<span data-ttu-id="1e7c4-192">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-192">Windows</span></span> |
| <span data-ttu-id="1e7c4-193">[Удаленный рабочий стол](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="1e7c4-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="1e7c4-194">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-194">✔</span></span> |<span data-ttu-id="1e7c4-195">✔</span><span class="sxs-lookup"><span data-stu-id="1e7c4-195">✔</span></span> |<span data-ttu-id="1e7c4-196">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-196">Windows</span></span> |<span data-ttu-id="1e7c4-197">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7c4-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1e7c4-198">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1e7c4-199">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1e7c4-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="1e7c4-200">Использование Pig и SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="1e7c4-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="1e7c4-201">С помощью служб SQL Server Integration Services (SSIS) можно выполнить задание Pig.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="1e7c4-202">Пакет дополнительных компонентов Azure для служб SSIS предоставляет следующие компоненты, которые работают с заданиями Pig в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="1e7c4-203">[Задача Pig в Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="1e7c4-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="1e7c4-204">[Диспетчер подключений по подпискам Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="1e7c4-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="1e7c4-205">Узнать больше о пакете дополнительных компонентов Azure для служб SSIS можно [здесь][ssispack].</span><span class="sxs-lookup"><span data-stu-id="1e7c4-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="1e7c4-206"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e7c4-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="1e7c4-207">Теперь, когда вы узнали, как использовать Pig в HDInsight, воспользуйтесь следующими ссылками, чтобы изучить другие способы работы с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e7c4-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="1e7c4-208">[Отправка данных в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1e7c4-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1e7c4-209">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1e7c4-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="1e7c4-210">Использование Sqoop с HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e7c4-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="1e7c4-211">Использование Oozie с HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e7c4-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="1e7c4-212">[Использование заданий MapReduce с HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1e7c4-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
