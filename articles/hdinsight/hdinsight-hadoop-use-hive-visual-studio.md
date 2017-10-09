---
title: "aaaHive со средствами Озера данных (Hadoop) для Visual Studio — Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse hello Озера данных tools для Visual Studio toorun Apache Hive запросов с помощью Apache Hadoop в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7c248-103">Выполнять запросы Hive, с помощью средств hello Озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c248-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7c248-104">Узнайте, как Озера данных hello toouse tools для Visual Studio tooquery Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="7c248-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="7c248-105">Hello Озера данных средства позволяют tooeasily создавать, отправлять и отслеживать tooHadoop запросов Hive в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c248-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="7c248-106"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7c248-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7c248-107">Кластер Azure HDInsight (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="7c248-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7c248-108">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="7c248-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7c248-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7c248-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7c248-110">Visual Studio (один из следующих версий hello):</span><span class="sxs-lookup"><span data-stu-id="7c248-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="7c248-111">Visual Studio 2013 Community, Professional, Premium или Ultimate с обновлением 4</span><span class="sxs-lookup"><span data-stu-id="7c248-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="7c248-112">Visual Studio 2015 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="7c248-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="7c248-113">Visual Studio 2017 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="7c248-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="7c248-114">Средства HDInsight для Visual Studio или инструменты Azure Data Lake Tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c248-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="7c248-115">В разделе [приступить к работе со средствами Visual Studio Hadoop для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) сведения об установке и настройке средства hello.</span><span class="sxs-lookup"><span data-stu-id="7c248-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="7c248-116"><a id="run"></a>Выполнять запросы Hive, с помощью Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="7c248-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="7c248-117">Откройте **Visual Studio** и выберите **Создать** > **Проект** > **Azure Data Lake** > **HIVE** > **Hive Application** (Приложение Hive).</span><span class="sxs-lookup"><span data-stu-id="7c248-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="7c248-118">Введите имя этого проекта.</span><span class="sxs-lookup"><span data-stu-id="7c248-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="7c248-119">Откройте hello **Script.hql** файла, созданного с помощью этого проекта и вставить в следующие инструкции HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="7c248-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="7c248-120">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7c248-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7c248-121">`DROP TABLE`: Если hello таблица существует, эта инструкция удаляет его.</span><span class="sxs-lookup"><span data-stu-id="7c248-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="7c248-122">`CREATE EXTERNAL TABLE`: создает новую "внешнюю" таблицу в Hive.</span><span class="sxs-lookup"><span data-stu-id="7c248-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="7c248-123">Внешние таблицы хранить только определение таблицы hello в кусте (приветствия данные остаются в исходном расположении hello).</span><span class="sxs-lookup"><span data-stu-id="7c248-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="7c248-124">Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="7c248-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="7c248-125">Например, с помощью задания MapReduce или службы Azure.</span><span class="sxs-lookup"><span data-stu-id="7c248-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="7c248-126">Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="7c248-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="7c248-127">`ROW FORMAT`: Указывает способ форматирования hello данных Hive.</span><span class="sxs-lookup"><span data-stu-id="7c248-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="7c248-128">В этом случае hello полей в каждом журнале разделенные пробелом.</span><span class="sxs-lookup"><span data-stu-id="7c248-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="7c248-129">`STORED AS TEXTFILE LOCATION`: Указывает Hive там, где hello хранения данных (hello данные примера и каталог) и что он хранится в виде текста.</span><span class="sxs-lookup"><span data-stu-id="7c248-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="7c248-130">`SELECT`: Установите количество всех строк где столбца `t4` содержит значение hello `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="7c248-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="7c248-131">Эта инструкция должна вернуть значение `3`, так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="7c248-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="7c248-132">`INPUT__FILE__NAME LIKE '%.log'`: указывает Hive, что вернуть нужно только данные из файлов с расширением LOG.</span><span class="sxs-lookup"><span data-stu-id="7c248-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="7c248-133">Это предложение ограничивает hello toohello поиска sample.log файл, содержащий данные hello.</span><span class="sxs-lookup"><span data-stu-id="7c248-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="7c248-134">Выберите hello инструментов hello **кластера HDInsight** требуется toouse для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="7c248-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="7c248-135">Выберите **отправить** toorun hello инструкциях, как задание куста.</span><span class="sxs-lookup"><span data-stu-id="7c248-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Панель отправки](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="7c248-137">Hello **Hive Сводка заданий** появляется и отображает сведения о выполнении задания hello.</span><span class="sxs-lookup"><span data-stu-id="7c248-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="7c248-138">Используйте hello **обновление** toorefresh hello задания сведения о ссылке, пока hello **состояние задания** изменяет слишком**завершено**.</span><span class="sxs-lookup"><span data-stu-id="7c248-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![Сводка по завершенному заданию](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="7c248-140">Используйте hello **выходные данные задания** связать tooview hello выходные данные этого задания.</span><span class="sxs-lookup"><span data-stu-id="7c248-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="7c248-141">Он отображает `[ERROR] 3`, которое является значением hello, возвращаемых этим запросом.</span><span class="sxs-lookup"><span data-stu-id="7c248-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="7c248-142">Запросы Hive можно также отправлять без создания проекта.</span><span class="sxs-lookup"><span data-stu-id="7c248-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="7c248-143">С помощью **обозревателя сервера** разверните узлы **Azure** > **HDInsight**, щелкните правой кнопкой мыши сервер HDInsight, а затем выберите **Написать запрос Hive**.</span><span class="sxs-lookup"><span data-stu-id="7c248-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="7c248-144">В hello **temp.hql** документа, отображаемого, добавьте следующие инструкции HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="7c248-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="7c248-145">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7c248-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7c248-146">`CREATE TABLE IF NOT EXISTS`: создает таблицу, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="7c248-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="7c248-147">Поскольку hello `EXTERNAL` не используется ключевое слово, эта инструкция создает внутреннюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="7c248-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="7c248-148">Внутренние таблицы хранятся в хранилище данных Hive hello и управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="7c248-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7c248-149">В отличие от `EXTERNAL` таблиц, удаление внутренней таблицы также удаляет hello базовым данным.</span><span class="sxs-lookup"><span data-stu-id="7c248-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="7c248-150">`STORED AS ORC`-Сохраняет hello данных в табличном формате (ORC) оптимизированного строки.</span><span class="sxs-lookup"><span data-stu-id="7c248-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="7c248-151">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="7c248-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="7c248-152">`INSERT OVERWRITE ... SELECT`: Выбирает строки из hello `log4jLogs` таблицы, которые содержат `[ERROR]`, а затем вставки данных hello в hello `errorLogs` таблицы.</span><span class="sxs-lookup"><span data-stu-id="7c248-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="7c248-153">Панель инструментов hello, выберите **отправить** toorun hello задания.</span><span class="sxs-lookup"><span data-stu-id="7c248-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="7c248-154">Используйте hello **состояние задания** toodetermine hello задания успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="7c248-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="7c248-155">tooverify, hello задание создано hello таблицы, используйте **обозревателя серверов** и разверните **Azure** > **HDInsight** > кластеру HDInsight > **Баз данных hive** > **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="7c248-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="7c248-156">Hello **журналы ошибок** таблицы и hello **log4jLogs** , перечислены в таблице.</span><span class="sxs-lookup"><span data-stu-id="7c248-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="7c248-157"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c248-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7c248-158">Как можно видеть, hello средства HDInsight для Visual Studio предоставляют простой способ toowork с запросов Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7c248-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="7c248-159">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7c248-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="7c248-160">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c248-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="7c248-161">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7c248-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7c248-162">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c248-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="7c248-163">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c248-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7c248-164">Дополнительные сведения о hello средства HDInsight для Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7c248-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="7c248-165">Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive</span><span class="sxs-lookup"><span data-stu-id="7c248-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
