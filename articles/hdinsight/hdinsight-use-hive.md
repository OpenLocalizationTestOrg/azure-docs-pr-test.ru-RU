---
title: "aaaWhat — Apache Hive и HiveQL - Azure HDInsight | Документы Microsoft"
description: "Apache Hive — это система хранилища данных для Hadoop. Вы можете запрашивать данные, хранящиеся в кусте, с помощью HiveQL, аналогичные tooTransact-SQL. В этом документе, узнайте, как toouse Hive и HiveQL с Azure HDInsight."
keywords: "hiveql, какова куст hadoop hiveql hive, какова hive Узнайте, как toouse hive,"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="28908-106">Обзор Apache Hive и HiveQL в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="28908-107">[Apache Hive](http://hive.apache.org/) — это система хранилища данных для Hadoop.</span><span class="sxs-lookup"><span data-stu-id="28908-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="28908-108">Hive позволяет обобщать, запрашивать и анализировать данные.</span><span class="sxs-lookup"><span data-stu-id="28908-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="28908-109">HiveQL, являющийся аналогичные tooSQL языка запросов языке запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="28908-110">Куст позволяет tooproject структуры в значительной степени неструктурированных данных.</span><span class="sxs-lookup"><span data-stu-id="28908-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="28908-111">После определения структуры hello, можно использовать HiveQL tooquery hello данных без ведома Java или MapReduce.</span><span class="sxs-lookup"><span data-stu-id="28908-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="28908-112">HDInsight предоставляет несколько типов кластера, которые подходят для конкретных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="28908-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="28908-113">следующие типы кластера Hello чаще всего используются для запросов Hive:</span><span class="sxs-lookup"><span data-stu-id="28908-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="28908-114">__Интерактивный куст__: кластера Hadoop, который предоставляет [Низкая задержка аналитической обработки (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) время ответа tooimprove функциональные возможности для интерактивной обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="28908-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="28908-115">Дополнительные сведения см. в разделе hello [начинаться с интерактивной Hive в HDInsight](hdinsight-hadoop-use-interactive-hive.md) документа.</span><span class="sxs-lookup"><span data-stu-id="28908-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="28908-116">__Hadoop:__ кластер Hadoop, который предназначен для рабочих нагрузок пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="28908-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="28908-117">Дополнительные сведения см. в разделе hello [начинаться с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) документа.</span><span class="sxs-lookup"><span data-stu-id="28908-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="28908-118">__Spark:__ Apache Spark содержит встроенные функциональные возможности для работы с Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="28908-119">Дополнительные сведения см. в разделе hello [начать с Spark в HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) документа.</span><span class="sxs-lookup"><span data-stu-id="28908-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="28908-120">__HBase__: HiveQL может быть tooquery используемые данные, хранящиеся в HBase.</span><span class="sxs-lookup"><span data-stu-id="28908-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="28908-121">Дополнительные сведения см. в разделе hello [начинаться с HBase на HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) документа.</span><span class="sxs-lookup"><span data-stu-id="28908-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="28908-122">Как toouse Hive</span><span class="sxs-lookup"><span data-stu-id="28908-122">How toouse Hive</span></span>

<span data-ttu-id="28908-123">Используйте следующие таблицы toodiscover как toouse Hive с HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="28908-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="28908-124">**Используйте этот метод**, если требуется:</span><span class="sxs-lookup"><span data-stu-id="28908-124">**Use this method** if you want...</span></span> | <span data-ttu-id="28908-125">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="28908-125">...an **interactive** shell</span></span> | <span data-ttu-id="28908-126">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="28908-126">...**batch** processing</span></span> | <span data-ttu-id="28908-127">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="28908-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="28908-128">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="28908-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="28908-129">Представление Hive</span><span class="sxs-lookup"><span data-stu-id="28908-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="28908-130">✔</span><span class="sxs-lookup"><span data-stu-id="28908-130">✔</span></span> |<span data-ttu-id="28908-131">✔</span><span class="sxs-lookup"><span data-stu-id="28908-131">✔</span></span> |<span data-ttu-id="28908-132">Linux</span><span class="sxs-lookup"><span data-stu-id="28908-132">Linux</span></span> |<span data-ttu-id="28908-133">Для приложений на основе браузера</span><span class="sxs-lookup"><span data-stu-id="28908-133">Any (browser based)</span></span> |
| [<span data-ttu-id="28908-134">клиент Beeline</span><span class="sxs-lookup"><span data-stu-id="28908-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="28908-135">✔</span><span class="sxs-lookup"><span data-stu-id="28908-135">✔</span></span> |<span data-ttu-id="28908-136">✔</span><span class="sxs-lookup"><span data-stu-id="28908-136">✔</span></span> |<span data-ttu-id="28908-137">Linux</span><span class="sxs-lookup"><span data-stu-id="28908-137">Linux</span></span> |<span data-ttu-id="28908-138">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="28908-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="28908-139">REST API</span><span class="sxs-lookup"><span data-stu-id="28908-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="28908-140">✔</span><span class="sxs-lookup"><span data-stu-id="28908-140">✔</span></span> |<span data-ttu-id="28908-141">Linux или Windows*</span><span class="sxs-lookup"><span data-stu-id="28908-141">Linux or Windows*</span></span> |<span data-ttu-id="28908-142">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="28908-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="28908-143">Средства HDInsight для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="28908-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="28908-144">✔</span><span class="sxs-lookup"><span data-stu-id="28908-144">✔</span></span> |<span data-ttu-id="28908-145">Linux или Windows*</span><span class="sxs-lookup"><span data-stu-id="28908-145">Linux or Windows*</span></span> |<span data-ttu-id="28908-146">Windows</span><span class="sxs-lookup"><span data-stu-id="28908-146">Windows</span></span> |
| [<span data-ttu-id="28908-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="28908-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="28908-148">✔</span><span class="sxs-lookup"><span data-stu-id="28908-148">✔</span></span> |<span data-ttu-id="28908-149">Linux или Windows*</span><span class="sxs-lookup"><span data-stu-id="28908-149">Linux or Windows*</span></span> |<span data-ttu-id="28908-150">Windows</span><span class="sxs-lookup"><span data-stu-id="28908-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="28908-151">\*Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="28908-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="28908-152">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="28908-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="28908-153">При использовании кластера HDInsight под управлением Windows, можно использовать hello [консоль запросов](hdinsight-hadoop-use-hive-query-console.md) из браузера или [удаленного рабочего стола](hdinsight-hadoop-use-hive-remote-desktop.md) toorun запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="28908-154">Справочник по языку HiveQL</span><span class="sxs-lookup"><span data-stu-id="28908-154">HiveQL language reference</span></span>

<span data-ttu-id="28908-155">Справочник по языку HiveQL доступен в hello [вручную языка (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="28908-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="28908-156">Hive и структура данных</span><span class="sxs-lookup"><span data-stu-id="28908-156">Hive and data structure</span></span>

<span data-ttu-id="28908-157">Куст понимает структуру toowork с и частично структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="28908-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="28908-158">Например текстовые файлы где hello поля разделены с определенных символов.</span><span class="sxs-lookup"><span data-stu-id="28908-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="28908-159">Привет, следующем за инструкцией HiveQL создает таблицу данных, разделенных пробелами:</span><span class="sxs-lookup"><span data-stu-id="28908-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="28908-160">Hive также поддерживает пользовательские **сериализаторы/десериализаторы (SerDe)** для сложных или беспорядочно структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="28908-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="28908-161">Дополнительные сведения см. в разделе hello [как toouse пользовательские SerDe JSON с HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) документа.</span><span class="sxs-lookup"><span data-stu-id="28908-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="28908-162">Дополнительные сведения о форматах файлов, поддерживаемых куста см. в разделе hello [вручную языка (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="28908-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="28908-163">Сравнение внутренних и внешних таблиц Hive</span><span class="sxs-lookup"><span data-stu-id="28908-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="28908-164">Существует два типа таблиц, которые вы можете создать с помощью Hive:</span><span class="sxs-lookup"><span data-stu-id="28908-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="28908-165">__Внутренняя__: данные хранятся в хранилище данных Hive hello.</span><span class="sxs-lookup"><span data-stu-id="28908-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="28908-166">Hello хранилища данных находится в `/hive/warehouse/` на hello хранилища по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="28908-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="28908-167">Используйте внутренние таблицы, если:</span><span class="sxs-lookup"><span data-stu-id="28908-167">Use internal tables when:</span></span>

    * <span data-ttu-id="28908-168">данные являются временными;</span><span class="sxs-lookup"><span data-stu-id="28908-168">Data is temporary.</span></span>
    * <span data-ttu-id="28908-169">Вы хотите куст toomanage hello жизненного цикла hello таблицы и данных.</span><span class="sxs-lookup"><span data-stu-id="28908-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="28908-170">__Внешние__: данные хранятся за пределами hello хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="28908-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="28908-171">Hello данные могут храниться в хранилище, доступное кластером hello.</span><span class="sxs-lookup"><span data-stu-id="28908-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="28908-172">Используйте внешние таблицы, если:</span><span class="sxs-lookup"><span data-stu-id="28908-172">Use external tables when:</span></span>

    * <span data-ttu-id="28908-173">Hello данные также используются за пределами Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="28908-174">Например файлы данных hello обновляются другим процессом (который не блокирует файлы hello.)</span><span class="sxs-lookup"><span data-stu-id="28908-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="28908-175">Данные должны tooremain в базовый расположения, даже после удаления таблицы hello hello.</span><span class="sxs-lookup"><span data-stu-id="28908-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="28908-176">вам нужно пользовательское расположение, например нестандартная учетная запись хранилища;</span><span class="sxs-lookup"><span data-stu-id="28908-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="28908-177">Программа, отличная от hive управляет hello формат данных, расположение и т. д.</span><span class="sxs-lookup"><span data-stu-id="28908-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="28908-178">Дополнительные сведения см. в разделе hello [Hive внутренних и внешних таблиц начальный] [ cindygross-hive-tables] записи блога.</span><span class="sxs-lookup"><span data-stu-id="28908-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="28908-179">Определяемые пользователем функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="28908-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="28908-180">Инфраструктура Hive также может быть расширена с помощью **определяемых пользователем функций (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="28908-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="28908-181">Определяемая пользователем Функция позволяет tooimplement функциональность или логику, которая не легко моделируется в HiveQL.</span><span class="sxs-lookup"><span data-stu-id="28908-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="28908-182">Пример использования определяемых пользователем функций с Hive см. следующие документы hello:</span><span class="sxs-lookup"><span data-stu-id="28908-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="28908-183">Работа с определяемыми пользователем функциями Java с использованием Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="28908-184">Использование пользовательских функций Python с Hive и Pig в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="28908-185">Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="28908-186">Как tooadd пользовательские Hive определяемой пользователем функции tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="28908-187">Пример Hive определяемая пользователем функция tooconvert форматы даты и времени tooHive отметки времени</span><span class="sxs-lookup"><span data-stu-id="28908-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="28908-188"><a id="data"></a>Демонстрационные данные</span><span class="sxs-lookup"><span data-stu-id="28908-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="28908-189">Hive в HDInsight поставляется предварительно загруженным с внутренней таблицей `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="28908-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="28908-190">HDInsight также предоставляет пример наборов данных, которые могут использоваться с Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="28908-191">Эти наборы данных хранятся в hello `/example/data` и `/HdiSamples` каталоги.</span><span class="sxs-lookup"><span data-stu-id="28908-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="28908-192">Эти каталоги существуют в хранилище по умолчанию hello для кластера.</span><span class="sxs-lookup"><span data-stu-id="28908-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="28908-193"><a id="job"></a>Пример запроса Hive</span><span class="sxs-lookup"><span data-stu-id="28908-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="28908-194">Здравствуйте, следующие столбцы проекта операторы HiveQL hello `/example/data/sample.log` файла:</span><span class="sxs-lookup"><span data-stu-id="28908-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="28908-195">В предыдущем примере hello hello HiveQL инструкции выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="28908-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="28908-196">`set hive.execution.engine=tez;`: Задает hello toouse ядра выполнения Tez.</span><span class="sxs-lookup"><span data-stu-id="28908-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="28908-197">Использование Tez вместо MapReduce позволяет повысить производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="28908-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="28908-198">Дополнительные сведения о Tez см. в разделе hello [Tez Apache используется для повышения производительности](#usetez) раздела.</span><span class="sxs-lookup"><span data-stu-id="28908-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="28908-199">Эта инструкция необходима только при использовании кластера HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="28908-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="28908-200">Tez — подсистема выполнения по умолчанию hello для HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="28908-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="28908-201">`DROP TABLE`: Если hello таблица уже существует, удалите его.</span><span class="sxs-lookup"><span data-stu-id="28908-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="28908-202">`CREATE EXTERNAL TABLE`: создает новую **внешнюю** таблицу в Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="28908-203">Внешние таблицы в кусте хранить только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="28908-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="28908-204">Hello данных остается в исходном расположении hello и в исходном формате hello.</span><span class="sxs-lookup"><span data-stu-id="28908-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="28908-205">`ROW FORMAT`: Указывает способ форматирования hello данных Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="28908-206">В этом случае hello полей в каждом журнале разделенные пробелом.</span><span class="sxs-lookup"><span data-stu-id="28908-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="28908-207">`STORED AS TEXTFILE LOCATION`: Указывает Hive там, где hello хранения данных (hello `example/data` directory) и что он хранится в виде текста.</span><span class="sxs-lookup"><span data-stu-id="28908-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="28908-208">Hello данные в одном файле или распределены по нескольким файлам в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="28908-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="28908-209">`SELECT`: Выбирает число всех строк, где hello столбца **t4** содержит значение hello **[ошибка]**.</span><span class="sxs-lookup"><span data-stu-id="28908-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="28908-210">Эта инструкция должна вернуть значение **3**, так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="28908-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="28908-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive попыток tooapply hello схемы tooall файлы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="28908-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="28908-212">В этом случае hello каталог содержит файлы, не соответствующие схеме hello.</span><span class="sxs-lookup"><span data-stu-id="28908-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="28908-213">tooprevent данных сборки мусора в результатах hello, этот оператор указывает Hive, мы должны возвращать только данные из файлы которых заканчиваются. журнала.</span><span class="sxs-lookup"><span data-stu-id="28908-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="28908-214">Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="28908-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="28908-215">Например, процессом автоматизированной передачи данных или другой операцией MapReduce.</span><span class="sxs-lookup"><span data-stu-id="28908-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="28908-216">Удаление внешней таблицы **не** удаление данных hello удаляет только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="28908-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="28908-217">toocreate **внутренней** вместо внешней таблицы, используйте следующие HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="28908-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="28908-218">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="28908-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="28908-219">`CREATE TABLE IF NOT EXISTS`: Если hello таблица не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="28908-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="28908-220">Поскольку hello **ВНЕШНИХ** не используется ключевое слово, эта инструкция создает внутреннюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="28908-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="28908-221">Hello таблица хранится в хранилище данных Hive hello и полностью управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="28908-222">`STORED AS ORC`: Хранит данные hello оптимизированными строк по столбцам (формат ORC.).</span><span class="sxs-lookup"><span data-stu-id="28908-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="28908-223">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="28908-224">`INSERT OVERWRITE ... SELECT`: Выбирает строки из hello **log4jLogs** таблицу, содержащую **[ошибка]**, а затем вставляет hello данных в hello **журналы ошибок** таблицы.</span><span class="sxs-lookup"><span data-stu-id="28908-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="28908-225">В отличие от внешних таблиц удаление внутренней таблицы также будут удалены hello базовых данных.</span><span class="sxs-lookup"><span data-stu-id="28908-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="28908-226">Повышение производительности запросов Hive</span><span class="sxs-lookup"><span data-stu-id="28908-226">Improve Hive query performance</span></span>

### <span data-ttu-id="28908-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="28908-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="28908-228">[Apache Tez](http://tez.apache.org) — платформа, которая позволяет приложения с большим объемом данных, например Hive toorun гораздо эффективнее в масштабе.</span><span class="sxs-lookup"><span data-stu-id="28908-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="28908-229">По умолчанию Tez включена для кластеров HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="28908-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="28908-230">В настоящее время Tez по умолчанию отключена для кластеров HDInsight под управлением Windows. Необходимо включить эту платформу.</span><span class="sxs-lookup"><span data-stu-id="28908-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="28908-231">для запроса Hive должны устанавливаться tootake преимуществами Tez hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="28908-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="28908-232">Tez — механизм по умолчанию hello для кластеров HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="28908-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="28908-233">Hello [Hive в документах разработки Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) содержит подробные сведения о реализации вариантов hello и настройки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="28908-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="28908-234">tooaid при отладке заданий выполнялась с использованием Tez, HDInsight предоставляет следующие пользовательских веб-интерфейсов, позволяющих tooview подробные сведения о заданиях Tez hello:</span><span class="sxs-lookup"><span data-stu-id="28908-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="28908-235">Использовать hello Ambari Tez представление на основе Linux HDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="28908-236">Использовать hello Tez пользовательского интерфейса на основе Windows HDInsight</span><span class="sxs-lookup"><span data-stu-id="28908-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="28908-237">Аналитическая обработка с низкой задержкой (LLAP)</span><span class="sxs-lookup"><span data-stu-id="28908-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="28908-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (иногда называемая Live Long and Process) — это новая функция в Hive 2.0, которая разрешает кэширование запросов в памяти.</span><span class="sxs-lookup"><span data-stu-id="28908-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="28908-239">LLAP делает запросы Hive значительно быстрее, копирование слишком[26 x быстрее, чем Hive 1.x в некоторых случаях](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="28908-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="28908-240">HDInsight предоставляет LLAP hello тип интерактивный Hive кластера.</span><span class="sxs-lookup"><span data-stu-id="28908-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="28908-241">Дополнительные сведения см. в разделе hello [начинаться с интерактивной Hive](hdinsight-hadoop-use-interactive-hive.md) документа.</span><span class="sxs-lookup"><span data-stu-id="28908-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="28908-242">Задания Pig и SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="28908-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="28908-243">Можно использовать SQL Server Integration Services (SSIS) toorun задания Hive.</span><span class="sxs-lookup"><span data-stu-id="28908-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="28908-244">пакет дополнительных компонентов Azure для служб SSIS Hello предоставляет следующие компоненты, которые работают с задания Hive в HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="28908-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="28908-245">[Задача Hive в Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="28908-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="28908-246">[Диспетчер подключений по подпискам Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="28908-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="28908-247">Дополнительные сведения о hello пакет дополнительных компонентов Azure для служб SSIS [здесь][ssispack].</span><span class="sxs-lookup"><span data-stu-id="28908-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="28908-248"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28908-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="28908-249">Теперь, когда вы узнали куст — и как toouse на Hadoop в HDInsight hello используйте следующие ссылки tooexplore toowork другими способами с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28908-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="28908-250">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="28908-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="28908-251">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="28908-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="28908-252">[Использование заданий MapReduce с HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="28908-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
