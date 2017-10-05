---
title: "Основные сведения об Apache Hive и HiveQL в Azure HDInsight | Документация Майкрософт"
description: "Apache Hive — это система хранилища данных для Hadoop. Вы можете запрашивать данные, хранящиеся в Hive, с помощью HiveQL, который напоминает Transact-SQL. В рамках этого руководства вы узнаете, как использовать Hive и HiveQL в Azure HDInsight."
keywords: "hiveql, что такое hive, hadoop hiveql, как использовать hive, знакомство с hive, обзор hive"
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
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="87632-106">Обзор Apache Hive и HiveQL в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="87632-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="87632-107">[Apache Hive](http://hive.apache.org/) — это система хранилища данных для Hadoop.</span><span class="sxs-lookup"><span data-stu-id="87632-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="87632-108">Hive позволяет обобщать, запрашивать и анализировать данные.</span><span class="sxs-lookup"><span data-stu-id="87632-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="87632-109">Запросы Hive создаются на языке запросов HiveQL, который похож на SQL.</span><span class="sxs-lookup"><span data-stu-id="87632-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="87632-110">Hive позволяет создавать структуру для преимущественно неструктурированных данных.</span><span class="sxs-lookup"><span data-stu-id="87632-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="87632-111">После определения структуры вы можете использовать HiveQL для запроса этих данных без знания Java или MapReduce.</span><span class="sxs-lookup"><span data-stu-id="87632-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="87632-112">HDInsight предоставляет несколько типов кластера, которые подходят для конкретных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="87632-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="87632-113">Для запросов Hive наиболее часто используются следующие типы кластеров:</span><span class="sxs-lookup"><span data-stu-id="87632-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="87632-114">__Interactive Hive:__ кластер Hadoop, который обеспечивает функцию [аналитической обработки с низкой задержкой (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) для оптимизации времени ответа для интерактивных запросов.</span><span class="sxs-lookup"><span data-stu-id="87632-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="87632-115">Дополнительные сведения см. в статье [Использование Interactive Hive в HDInsight (предварительная версия)](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="87632-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="87632-116">__Hadoop:__ кластер Hadoop, который предназначен для рабочих нагрузок пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="87632-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="87632-117">Дополнительные сведения см. в статье [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="87632-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="87632-118">__Spark:__ Apache Spark содержит встроенные функциональные возможности для работы с Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="87632-119">Дополнительные сведения см. в статье [Начало работы. Создание кластера Apache Spark в Azure HDInsight и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="87632-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="87632-120">__HBase:__ HiveQL может использоваться для запроса данных, хранящихся в HBase.</span><span class="sxs-lookup"><span data-stu-id="87632-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="87632-121">Дополнительные сведения см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Linux в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="87632-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="87632-122">Как использовать Hive</span><span class="sxs-lookup"><span data-stu-id="87632-122">How to use Hive</span></span>

<span data-ttu-id="87632-123">Используйте следующую таблицу, чтобы узнать, как использовать Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="87632-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="87632-124">**Используйте этот метод**, если требуется:</span><span class="sxs-lookup"><span data-stu-id="87632-124">**Use this method** if you want...</span></span> | <span data-ttu-id="87632-125">... **интерактивная** оболочка</span><span class="sxs-lookup"><span data-stu-id="87632-125">...an **interactive** shell</span></span> | <span data-ttu-id="87632-126">...**пакетная** обработка</span><span class="sxs-lookup"><span data-stu-id="87632-126">...**batch** processing</span></span> | <span data-ttu-id="87632-127">...with этим **кластером операционной системы**</span><span class="sxs-lookup"><span data-stu-id="87632-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="87632-128">...из этого **кластера операционной системы**</span><span class="sxs-lookup"><span data-stu-id="87632-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="87632-129">Представление Hive</span><span class="sxs-lookup"><span data-stu-id="87632-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="87632-130">✔</span><span class="sxs-lookup"><span data-stu-id="87632-130">✔</span></span> |<span data-ttu-id="87632-131">✔</span><span class="sxs-lookup"><span data-stu-id="87632-131">✔</span></span> |<span data-ttu-id="87632-132">Linux</span><span class="sxs-lookup"><span data-stu-id="87632-132">Linux</span></span> |<span data-ttu-id="87632-133">Для приложений на основе браузера</span><span class="sxs-lookup"><span data-stu-id="87632-133">Any (browser based)</span></span> |
| [<span data-ttu-id="87632-134">клиент Beeline</span><span class="sxs-lookup"><span data-stu-id="87632-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="87632-135">✔</span><span class="sxs-lookup"><span data-stu-id="87632-135">✔</span></span> |<span data-ttu-id="87632-136">✔</span><span class="sxs-lookup"><span data-stu-id="87632-136">✔</span></span> |<span data-ttu-id="87632-137">Linux</span><span class="sxs-lookup"><span data-stu-id="87632-137">Linux</span></span> |<span data-ttu-id="87632-138">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="87632-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="87632-139">REST API</span><span class="sxs-lookup"><span data-stu-id="87632-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="87632-140">✔</span><span class="sxs-lookup"><span data-stu-id="87632-140">✔</span></span> |<span data-ttu-id="87632-141">Linux или Windows*</span><span class="sxs-lookup"><span data-stu-id="87632-141">Linux or Windows*</span></span> |<span data-ttu-id="87632-142">Linux, Unix, Mac OS X или Windows</span><span class="sxs-lookup"><span data-stu-id="87632-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="87632-143">Средства HDInsight для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87632-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="87632-144">✔</span><span class="sxs-lookup"><span data-stu-id="87632-144">✔</span></span> |<span data-ttu-id="87632-145">Linux или Windows*</span><span class="sxs-lookup"><span data-stu-id="87632-145">Linux or Windows*</span></span> |<span data-ttu-id="87632-146">Windows</span><span class="sxs-lookup"><span data-stu-id="87632-146">Windows</span></span> |
| [<span data-ttu-id="87632-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="87632-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="87632-148">✔</span><span class="sxs-lookup"><span data-stu-id="87632-148">✔</span></span> |<span data-ttu-id="87632-149">Linux или Windows*</span><span class="sxs-lookup"><span data-stu-id="87632-149">Linux or Windows*</span></span> |<span data-ttu-id="87632-150">Windows</span><span class="sxs-lookup"><span data-stu-id="87632-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="87632-151">\* Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="87632-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="87632-152">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="87632-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="87632-153">Если вы используете кластер HDInsight на платформе Windows, вы можете использовать [консоль запросов](hdinsight-hadoop-use-hive-query-console.md) в браузере или [удаленный рабочий стол](hdinsight-hadoop-use-hive-remote-desktop.md) для выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="87632-154">Справочник по языку HiveQL</span><span class="sxs-lookup"><span data-stu-id="87632-154">HiveQL language reference</span></span>

<span data-ttu-id="87632-155">Справочник по языку HiveQL доступен на странице [LanguageManual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="87632-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="87632-156">Hive и структура данных</span><span class="sxs-lookup"><span data-stu-id="87632-156">Hive and data structure</span></span>

<span data-ttu-id="87632-157">Hive поддерживает работу со структурированными и частично структурированными данными.</span><span class="sxs-lookup"><span data-stu-id="87632-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="87632-158">Например, с текстовыми файлами, в которых поля разделяются с помощью определенных знаков.</span><span class="sxs-lookup"><span data-stu-id="87632-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="87632-159">С помощью следующей инструкции HiveQL создается таблица для данных, разделенных пробелами:</span><span class="sxs-lookup"><span data-stu-id="87632-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="87632-160">Hive также поддерживает пользовательские **сериализаторы/десериализаторы (SerDe)** для сложных или беспорядочно структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="87632-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="87632-161">Дополнительные сведения см. в документе [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) (Как использовать настраиваемую сериализацию-десериализациюJSON с HDInsight).</span><span class="sxs-lookup"><span data-stu-id="87632-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="87632-162">Дополнительные сведения о форматах файлов, поддерживаемых Hive, см. на странице [LanguageManual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="87632-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="87632-163">Сравнение внутренних и внешних таблиц Hive</span><span class="sxs-lookup"><span data-stu-id="87632-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="87632-164">Существует два типа таблиц, которые вы можете создать с помощью Hive:</span><span class="sxs-lookup"><span data-stu-id="87632-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="87632-165">__Внутренняя:__ данные хранятся в хранилище данных Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="87632-166">Хранилище данных расположено в `/hive/warehouse/`, в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="87632-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="87632-167">Используйте внутренние таблицы, если:</span><span class="sxs-lookup"><span data-stu-id="87632-167">Use internal tables when:</span></span>

    * <span data-ttu-id="87632-168">данные являются временными;</span><span class="sxs-lookup"><span data-stu-id="87632-168">Data is temporary.</span></span>
    * <span data-ttu-id="87632-169">вы хотите использовать Hive для управления жизненным циклом таблицы и данных.</span><span class="sxs-lookup"><span data-stu-id="87632-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="87632-170">__Внешняя:__ данные хранятся за пределами хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="87632-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="87632-171">Данные могут храниться в любом хранилище, доступном для кластера.</span><span class="sxs-lookup"><span data-stu-id="87632-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="87632-172">Используйте внешние таблицы, если:</span><span class="sxs-lookup"><span data-stu-id="87632-172">Use external tables when:</span></span>

    * <span data-ttu-id="87632-173">данные также используются за пределами Hive</span><span class="sxs-lookup"><span data-stu-id="87632-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="87632-174">(например, файлы данных обновляются с помощью другого процесса, который не блокирует их);</span><span class="sxs-lookup"><span data-stu-id="87632-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="87632-175">данные должны оставаться в базовом расположении даже после удаления таблицы;</span><span class="sxs-lookup"><span data-stu-id="87632-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="87632-176">вам нужно пользовательское расположение, например нестандартная учетная запись хранилища;</span><span class="sxs-lookup"><span data-stu-id="87632-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="87632-177">программа, отличная от Hive, управляет форматом данных, расположением и т. д.</span><span class="sxs-lookup"><span data-stu-id="87632-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="87632-178">Дополнительные сведения см. в записи блога [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables] (HDInsight: введение во внутренние и внешние таблицы Hive).</span><span class="sxs-lookup"><span data-stu-id="87632-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="87632-179">Определяемые пользователем функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="87632-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="87632-180">Инфраструктура Hive также может быть расширена с помощью **определяемых пользователем функций (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="87632-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="87632-181">UDF позволяет реализовать функции или логику, сложно моделируемые в HiveQL.</span><span class="sxs-lookup"><span data-stu-id="87632-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="87632-182">Примеры использования определяемых пользователем функций с Hive приведены в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="87632-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="87632-183">Работа с определяемыми пользователем функциями Java с использованием Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="87632-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="87632-184">Использование пользовательских функций Python с Hive и Pig в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="87632-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="87632-185">Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="87632-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* <span data-ttu-id="87632-186">[How to add custom Hive UDFs to HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx) (Как добавить настраиваемые определяемые пользователем функции Hive в HDInsight)</span><span class="sxs-lookup"><span data-stu-id="87632-186">[How to add a custom Hive user-defined function to HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)</span></span>

* [<span data-ttu-id="87632-187">Пример определяемой пользователем функции Hive для преобразования форматов даты и времени в метки времени Hive</span><span class="sxs-lookup"><span data-stu-id="87632-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="87632-188"><a id="data"></a>Демонстрационные данные</span><span class="sxs-lookup"><span data-stu-id="87632-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="87632-189">Hive в HDInsight поставляется предварительно загруженным с внутренней таблицей `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="87632-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="87632-190">HDInsight также предоставляет пример наборов данных, которые могут использоваться с Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="87632-191">Эти наборы данных хранятся в каталогах `/example/data` и `/HdiSamples`.</span><span class="sxs-lookup"><span data-stu-id="87632-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="87632-192">Эти каталоги находятся в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="87632-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="87632-193"><a id="job"></a>Пример запроса Hive</span><span class="sxs-lookup"><span data-stu-id="87632-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="87632-194">Приведенная ниже инструкция HiveQL проецирует столбцы проекта в файл `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="87632-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="87632-195">В предыдущем примере операторы HiveQL выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87632-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="87632-196">`set hive.execution.engine=tez;`: задает механизм выполнения с использованием Tez.</span><span class="sxs-lookup"><span data-stu-id="87632-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="87632-197">Использование Tez вместо MapReduce позволяет повысить производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="87632-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="87632-198">Дополнительные сведения о Tez см. в разделе [Использование Apache Tez для повышения производительности](#usetez).</span><span class="sxs-lookup"><span data-stu-id="87632-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="87632-199">Эта инструкция необходима только при использовании кластера HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="87632-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="87632-200">Tez является подсистемой выполнения по умолчанию для HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="87632-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="87632-201">`DROP TABLE`: если таблица уже существует, удалите ее.</span><span class="sxs-lookup"><span data-stu-id="87632-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="87632-202">`CREATE EXTERNAL TABLE`: создает новую **внешнюю** таблицу в Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="87632-203">Внешние таблицы хранят только определения таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="87632-204">Данные остаются в исходном расположении и формате.</span><span class="sxs-lookup"><span data-stu-id="87632-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="87632-205">`ROW FORMAT`: инструкции по форматированию данных для Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="87632-206">В данном случае поля всех журналов разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="87632-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="87632-207">`STORED AS TEXTFILE LOCATION`: указывает Hive расположение хранения данных (каталог `example/data`) и их формат (текст).</span><span class="sxs-lookup"><span data-stu-id="87632-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="87632-208">Данные могут храниться в одном файле или быть распределенными по нескольким файлам в каталоге.</span><span class="sxs-lookup"><span data-stu-id="87632-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="87632-209">`SELECT`: подсчитывает количество всех строк, в которых столбец **t4** содержит значение **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="87632-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="87632-210">Эта инструкция должна вернуть значение **3**, так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="87632-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="87632-211">`INPUT__FILE__NAME LIKE '%.log'`. Hive пытается применить схему ко всем файлам в каталоге.</span><span class="sxs-lookup"><span data-stu-id="87632-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="87632-212">В этом случае каталог содержит файлы, которые не соответствуют схеме.</span><span class="sxs-lookup"><span data-stu-id="87632-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="87632-213">Чтобы исключить лишние данные в результатах, эта инструкция указывает Hive возвращать данные только из файлов, заканчивающихся на .log.</span><span class="sxs-lookup"><span data-stu-id="87632-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="87632-214">Внешние таблицы следует использовать, если исходные данные должны обновляться с использованием внешних источников.</span><span class="sxs-lookup"><span data-stu-id="87632-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="87632-215">Например, процессом автоматизированной передачи данных или другой операцией MapReduce.</span><span class="sxs-lookup"><span data-stu-id="87632-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="87632-216">Удаление внешней таблицы **не** приводит к удалению данных; будет удалено только описание таблицы.</span><span class="sxs-lookup"><span data-stu-id="87632-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="87632-217">Для создания **внутренней** таблицы вместо внешней используйте следующий запрос HiveQL.</span><span class="sxs-lookup"><span data-stu-id="87632-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="87632-218">Эти операторы выполняют следующие действия:</span><span class="sxs-lookup"><span data-stu-id="87632-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="87632-219">`CREATE TABLE IF NOT EXISTS`: если таблица не существует, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="87632-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="87632-220">Так как ключевое слово **EXTERNAL** не используется, эта инструкция создает внутреннюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="87632-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="87632-221">Таблица хранится в хранилище данных Hive и полностью управляется Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="87632-222">`STORED AS ORC`: позволяет сохранить данные в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="87632-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="87632-223">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="87632-224">`INSERT OVERWRITE ... SELECT`: выбирает строки из таблицы **log4jLogs**, содержащей значение **[ERROR]**, а затем вставляет данные в таблицу **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="87632-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="87632-225">В отличие от внешних таблиц, удаление внутренней таблицы приводит к удалению базовых данных.</span><span class="sxs-lookup"><span data-stu-id="87632-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="87632-226">Повышение производительности запросов Hive</span><span class="sxs-lookup"><span data-stu-id="87632-226">Improve Hive query performance</span></span>

### <span data-ttu-id="87632-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="87632-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="87632-228">[Apache Tez](http://tez.apache.org) — это платформа, которая позволяет повысить производительность приложений, обрабатывающих большие объемы данных (включая Hive).</span><span class="sxs-lookup"><span data-stu-id="87632-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="87632-229">По умолчанию Tez включена для кластеров HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="87632-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="87632-230">В настоящее время Tez по умолчанию отключена для кластеров HDInsight под управлением Windows. Необходимо включить эту платформу.</span><span class="sxs-lookup"><span data-stu-id="87632-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="87632-231">Чтобы воспользоваться преимуществами работы с Tez, необходимо установить для запроса Hive следующие значения переменных:</span><span class="sxs-lookup"><span data-stu-id="87632-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="87632-232">Tez является подсистемой по умолчанию для кластеров HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="87632-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="87632-233">Раздел [Документация по работе Hive на Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) содержит дополнительные сведения о реализации этого решения и вариантах настроек.</span><span class="sxs-lookup"><span data-stu-id="87632-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="87632-234">Для помощи в отладке заданий, запущенных с помощью Tez, HDInsight предоставляет следующие веб-интерфейсы, позволяющие просмотреть сведения о заданиях Tez:</span><span class="sxs-lookup"><span data-stu-id="87632-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="87632-235">Использование представления Ambari Tez в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="87632-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="87632-236">Использование пользовательского интерфейса Tez в HDInsight на платформе Windows</span><span class="sxs-lookup"><span data-stu-id="87632-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="87632-237">Аналитическая обработка с низкой задержкой (LLAP)</span><span class="sxs-lookup"><span data-stu-id="87632-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="87632-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (иногда называемая Live Long and Process) — это новая функция в Hive 2.0, которая разрешает кэширование запросов в памяти.</span><span class="sxs-lookup"><span data-stu-id="87632-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="87632-239">LLAP создает запросы Hive гораздо быстрее — в [некоторых случаях в 26 раз быстрее, чем Hive версии 1.x](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="87632-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="87632-240">HDInsight предоставляет LLAP в кластере Hive интерактивного типа.</span><span class="sxs-lookup"><span data-stu-id="87632-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="87632-241">Дополнительные сведения см. в статье [Использование Interactive Hive в HDInsight (предварительная версия)](hdinsight-hadoop-use-interactive-hive.md).</span><span class="sxs-lookup"><span data-stu-id="87632-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="87632-242">Задания Pig и SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="87632-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="87632-243">С помощью служб SQL Server Integration Services (SSIS) можно выполнить задание Hive.</span><span class="sxs-lookup"><span data-stu-id="87632-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="87632-244">Пакет дополнительных компонентов Azure для служб SSIS предоставляет следующие компоненты, которые работают с заданиями Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87632-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="87632-245">[Задача Hive в Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="87632-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="87632-246">[Диспетчер подключений по подпискам Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="87632-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="87632-247">Узнать больше о пакете дополнительных компонентов Azure для служб SSIS можно [здесь][ssispack].</span><span class="sxs-lookup"><span data-stu-id="87632-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="87632-248"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87632-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="87632-249">Теперь, когда вы знаете, что такое инфраструктура Hive и как ее использовать с Hadoop в HDInsight, воспользуйтесь следующими ссылками, чтобы изучить другие способы работы с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87632-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="87632-250">[Отправка данных в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="87632-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="87632-251">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="87632-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="87632-252">[Использование заданий MapReduce с HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="87632-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
