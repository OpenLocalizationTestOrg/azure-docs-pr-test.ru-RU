---
title: "aaaUse Pig для Hadoop в HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Pig с Hadoop в HDInsight."
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
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="9c1ee-103">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c1ee-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="9c1ee-104">Узнайте, как toouse [Apache Pig](http://pig.apache.org/) с HDInsight...</span><span class="sxs-lookup"><span data-stu-id="9c1ee-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="9c1ee-105">Pig — это платформа, позволяющая создавать программы для Hadoop с помощью процедурного языка, известного как *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="9c1ee-106">Pig является альтернативным tooJava для создания *MapReduce* решений, который входит в состав Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="9c1ee-107">Используйте следующие таблицы toodiscover hello различные способы использования Pig с HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="9c1ee-108">**Используйте** , если требуется...</span><span class="sxs-lookup"><span data-stu-id="9c1ee-108">**Use this** if you want...</span></span> | <span data-ttu-id="9c1ee-109">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="9c1ee-109">...an **interactive** shell</span></span> | <span data-ttu-id="9c1ee-110">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="9c1ee-110">...**batch** processing</span></span> | <span data-ttu-id="9c1ee-111">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="9c1ee-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="9c1ee-112">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="9c1ee-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="9c1ee-113">SSH</span><span class="sxs-lookup"><span data-stu-id="9c1ee-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="9c1ee-114">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-114">✔</span></span> |<span data-ttu-id="9c1ee-115">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-115">✔</span></span> |<span data-ttu-id="9c1ee-116">Linux</span><span class="sxs-lookup"><span data-stu-id="9c1ee-116">Linux</span></span> |<span data-ttu-id="9c1ee-117">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9c1ee-118">REST API</span><span class="sxs-lookup"><span data-stu-id="9c1ee-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="9c1ee-119">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-119">✔</span></span> |<span data-ttu-id="9c1ee-120">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-120">Linux or Windows</span></span> |<span data-ttu-id="9c1ee-121">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9c1ee-122">.NET SDK для Hadoop</span><span class="sxs-lookup"><span data-stu-id="9c1ee-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="9c1ee-123">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-123">✔</span></span> |<span data-ttu-id="9c1ee-124">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-124">Linux or Windows</span></span> |<span data-ttu-id="9c1ee-125">Windows (сейчас)</span><span class="sxs-lookup"><span data-stu-id="9c1ee-125">Windows (for now)</span></span> |
| [<span data-ttu-id="9c1ee-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c1ee-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="9c1ee-127">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-127">✔</span></span> |<span data-ttu-id="9c1ee-128">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-128">Linux or Windows</span></span> |<span data-ttu-id="9c1ee-129">Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-129">Windows</span></span> |
| <span data-ttu-id="9c1ee-130">[Удаленный рабочий стол](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="9c1ee-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="9c1ee-131">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-131">✔</span></span> |<span data-ttu-id="9c1ee-132">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-132">✔</span></span> |<span data-ttu-id="9c1ee-133">Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-133">Windows</span></span> |<span data-ttu-id="9c1ee-134">Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9c1ee-135">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9c1ee-136">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9c1ee-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9c1ee-137"><a id="why"></a>Почему именно Pig?</span><span class="sxs-lookup"><span data-stu-id="9c1ee-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="9c1ee-138">Одна из проблем hello обработки данных с помощью MapReduce в Hadoop реализует логику обработки, используя только схему и функцию сокращения.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="9c1ee-139">Для обработки сложных, вы часто имеют toobreak обработки в нескольких MapReduce операции, которые будут соединены друг с другом tooachieve hello требуемого результата.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="9c1ee-140">Pig позволяет toodefine обработки как набор преобразований, потоки данных через выходной hello требуемого tooproduce hello.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="9c1ee-141">язык Pig латиница Hello позволяет вам toodescribe hello поток данных из необработанные данные ввода через один или несколько преобразования, вывода tooproduce требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="9c1ee-142">Программы Pig Latin следуют общему шаблону:</span><span class="sxs-lookup"><span data-stu-id="9c1ee-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="9c1ee-143">**Загрузка**: чтение данных toobe с hello файловой системы</span><span class="sxs-lookup"><span data-stu-id="9c1ee-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="9c1ee-144">**Преобразование**: манипулировать данными hello</span><span class="sxs-lookup"><span data-stu-id="9c1ee-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="9c1ee-145">**Дамп или хранения**: вывод экрана toohello данных или сохранить его для обработки</span><span class="sxs-lookup"><span data-stu-id="9c1ee-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="9c1ee-146">Определяемые пользователем функции</span><span class="sxs-lookup"><span data-stu-id="9c1ee-146">User-defined functions</span></span>

<span data-ttu-id="9c1ee-147">Латинская pig также поддерживает определяемые пользователем функции (UDF), позволяющий tooinvoke внешние компоненты, реализующие логику, которая является сложным toomodel в Латинской Pig.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="9c1ee-148">Дополнительные сведения о Pig Latin см. в [справочном руководстве по Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) и [справочном руководстве по Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="9c1ee-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="9c1ee-149">Пример использования определяемых пользователем функций с Pig см. следующие документы hello:</span><span class="sxs-lookup"><span data-stu-id="9c1ee-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="9c1ee-150">[Использование DataFu с Pig в HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) — DataFu представляет собой коллекцию полезных определяемых пользователем функций, поддерживаемых Apache</span><span class="sxs-lookup"><span data-stu-id="9c1ee-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="9c1ee-151">Использование Python с Pig и Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c1ee-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="9c1ee-152">Использование C# с Hive и Pig в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c1ee-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="9c1ee-153"><a id="data"></a>Демонстрационные данные</span><span class="sxs-lookup"><span data-stu-id="9c1ee-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="9c1ee-154">HDInsight предоставляет различные пример наборов данных, хранящихся в hello `/example/data` и `/HdiSamples` каталоги.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="9c1ee-155">Эти каталоги находятся в хранилище по умолчанию hello для кластера.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="9c1ee-156">Hello Pig в этом документе примере hello *log4j* файл из `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="9c1ee-157">Каждый журнал в файле hello состоит из полей строку, содержащую `[LOG LEVEL]` поле tooshow hello тип и hello степенью серьезности, например:</span><span class="sxs-lookup"><span data-stu-id="9c1ee-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="9c1ee-158">В предыдущем примере hello hello уровень ведения журнала — ошибка.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="9c1ee-159">Файл log4j можно также создать с помощью hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) средство ведения журнала, а затем передать файл tooyour большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="9c1ee-160">В разделе [tooHDInsight передача данных](hdinsight-upload-data.md) инструкции.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="9c1ee-161">Дополнительные сведения о том, каким образом большие двоичные объекты в службе хранилища Azure используются с HDInsight, см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9c1ee-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="9c1ee-162"><a id="job"></a>Пример задания</span><span class="sxs-lookup"><span data-stu-id="9c1ee-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="9c1ee-163">Hello следующее задание Pig латиница загружает hello `sample.log` файл из хранилища по умолчанию hello для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="9c1ee-164">Затем он выполняет серию преобразований, которые заканчиваются число как много раз входные данные уровня в hello каждого журнала.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="9c1ee-165">tooSTDOUT записываются результаты Hello.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="9c1ee-166">Hello следующем рисунке показана сводка какие каждое преобразование делает toohello данных.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Графическое представление преобразований hello][image-hdi-pig-data-transformation]

## <span data-ttu-id="9c1ee-168"><a id="run"></a>Запустить задание Pig латиница hello</span><span class="sxs-lookup"><span data-stu-id="9c1ee-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="9c1ee-169">HDInsight может запускать задания Pig Latin с помощью различных методов.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="9c1ee-170">Используйте следующие таблицы toodecide, какой метод подходит для вас hello, затем по ссылке hello Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="9c1ee-171">**Используйте** , если требуется...</span><span class="sxs-lookup"><span data-stu-id="9c1ee-171">**Use this** if you want...</span></span> | <span data-ttu-id="9c1ee-172">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="9c1ee-172">...an **interactive** shell</span></span> | <span data-ttu-id="9c1ee-173">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="9c1ee-173">...**batch** processing</span></span> | <span data-ttu-id="9c1ee-174">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="9c1ee-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="9c1ee-175">… в этом **клиенте**</span><span class="sxs-lookup"><span data-stu-id="9c1ee-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="9c1ee-176">SSH</span><span class="sxs-lookup"><span data-stu-id="9c1ee-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="9c1ee-177">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-177">✔</span></span> |<span data-ttu-id="9c1ee-178">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-178">✔</span></span> |<span data-ttu-id="9c1ee-179">Linux</span><span class="sxs-lookup"><span data-stu-id="9c1ee-179">Linux</span></span> |<span data-ttu-id="9c1ee-180">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9c1ee-181">Curl</span><span class="sxs-lookup"><span data-stu-id="9c1ee-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="9c1ee-182">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-182">✔</span></span> |<span data-ttu-id="9c1ee-183">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-183">Linux or Windows</span></span> |<span data-ttu-id="9c1ee-184">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9c1ee-185">.NET SDK для Hadoop</span><span class="sxs-lookup"><span data-stu-id="9c1ee-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="9c1ee-186">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-186">✔</span></span> |<span data-ttu-id="9c1ee-187">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-187">Linux or Windows</span></span> |<span data-ttu-id="9c1ee-188">Windows (сейчас)</span><span class="sxs-lookup"><span data-stu-id="9c1ee-188">Windows (for now)</span></span> |
| [<span data-ttu-id="9c1ee-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c1ee-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="9c1ee-190">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-190">✔</span></span> |<span data-ttu-id="9c1ee-191">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-191">Linux or Windows</span></span> |<span data-ttu-id="9c1ee-192">Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-192">Windows</span></span> |
| <span data-ttu-id="9c1ee-193">[Удаленный рабочий стол](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 и 3.3)</span><span class="sxs-lookup"><span data-stu-id="9c1ee-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="9c1ee-194">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-194">✔</span></span> |<span data-ttu-id="9c1ee-195">✔</span><span class="sxs-lookup"><span data-stu-id="9c1ee-195">✔</span></span> |<span data-ttu-id="9c1ee-196">Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-196">Windows</span></span> |<span data-ttu-id="9c1ee-197">Windows</span><span class="sxs-lookup"><span data-stu-id="9c1ee-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9c1ee-198">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9c1ee-199">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9c1ee-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="9c1ee-200">Использование Pig и SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="9c1ee-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="9c1ee-201">Можно использовать SQL Server Integration Services (SSIS) toorun задание Pig.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="9c1ee-202">пакет дополнительных компонентов Azure для служб SSIS Hello предоставляет следующие компоненты, которые работают с задания Pig в HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="9c1ee-203">[Задача Pig в Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="9c1ee-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="9c1ee-204">[Диспетчер подключений по подпискам Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="9c1ee-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="9c1ee-205">Дополнительные сведения о hello пакет дополнительных компонентов Azure для служб SSIS [здесь][ssispack].</span><span class="sxs-lookup"><span data-stu-id="9c1ee-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="9c1ee-206"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c1ee-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="9c1ee-207">Теперь, когда вы узнали, как toouse Pig с HDInsight, hello используйте следующие ссылки tooexplore toowork другими способами с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c1ee-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="9c1ee-208">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="9c1ee-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="9c1ee-209">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9c1ee-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="9c1ee-210">Использование Sqoop с HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c1ee-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="9c1ee-211">Использование Oozie с HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c1ee-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="9c1ee-212">[Использование заданий MapReduce с HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9c1ee-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
