---
title: "Использование Hive со Средствами Data Lake (Hadoop) для Visual Studio в Azure HDInsight | Документы Майкрософт"
description: "Узнайте, как использовать Средства Data Lake для Visual Studio с целью выполнения запросов Apache Hive с Apache Hadoop в Azure HDInsight."
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
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="dccc5-103">Выполнение запросов Hive с помощью Средств Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dccc5-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="dccc5-104">Узнайте, как использовать Средства Data Lake для Visual Studio с целью выполнения запросов Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="dccc5-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="dccc5-105">Средства Data Lake позволяют легко создавать, отправлять и отслеживать запросы Hive к Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dccc5-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="dccc5-106"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dccc5-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="dccc5-107">Кластер Azure HDInsight (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="dccc5-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="dccc5-108">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dccc5-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dccc5-109">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="dccc5-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="dccc5-110">Одна из следующих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="dccc5-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="dccc5-111">Visual Studio 2013 Community, Professional, Premium или Ultimate с обновлением 4</span><span class="sxs-lookup"><span data-stu-id="dccc5-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="dccc5-112">Visual Studio 2015 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="dccc5-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="dccc5-113">Visual Studio 2017 (любой выпуск)</span><span class="sxs-lookup"><span data-stu-id="dccc5-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="dccc5-114">Средства HDInsight для Visual Studio или инструменты Azure Data Lake Tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dccc5-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="dccc5-115">Пошаговые указания по установке и настройке инструментов Visual Studio Hadoop см. в статье [Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dccc5-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="dccc5-116"><a id="run"></a> Выполнение запросов Hive с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dccc5-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="dccc5-117">Откройте **Visual Studio** и выберите **Создать** > **Проект** > **Azure Data Lake** > **HIVE** > **Hive Application** (Приложение Hive).</span><span class="sxs-lookup"><span data-stu-id="dccc5-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="dccc5-118">Введите имя этого проекта.</span><span class="sxs-lookup"><span data-stu-id="dccc5-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="dccc5-119">Откройте файл **Script.hql** , созданный в этом проекте, и вставьте следующие операторы HiveQL:</span><span class="sxs-lookup"><span data-stu-id="dccc5-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="dccc5-120">Эти операторы выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dccc5-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="dccc5-121">`DROP TABLE`: если таблица существует, эта инструкция удаляет ее.</span><span class="sxs-lookup"><span data-stu-id="dccc5-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="dccc5-122">`CREATE EXTERNAL TABLE`: создает новую "внешнюю" таблицу в Hive.</span><span class="sxs-lookup"><span data-stu-id="dccc5-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="dccc5-123">Внешние таблицы хранят только определение самой таблицы в Hive, в то время как данные остаются в исходном расположении.</span><span class="sxs-lookup"><span data-stu-id="dccc5-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="dccc5-124">Внешние таблицы следует использовать, если исходные данные должны обновляться с использованием внешних источников.</span><span class="sxs-lookup"><span data-stu-id="dccc5-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="dccc5-125">Например, с помощью задания MapReduce или службы Azure.</span><span class="sxs-lookup"><span data-stu-id="dccc5-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="dccc5-126">Удаление внешней таблицы **не** приводит к удалению данных, будет удалено только определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="dccc5-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="dccc5-127">`ROW FORMAT`: инструкции по форматированию данных для Hive.</span><span class="sxs-lookup"><span data-stu-id="dccc5-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="dccc5-128">В данном случае поля всех журналов разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="dccc5-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="dccc5-129">`STORED AS TEXTFILE LOCATION`: указывает Hive расположение хранения данных (каталог example/data) и их формат (текст).</span><span class="sxs-lookup"><span data-stu-id="dccc5-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="dccc5-130">`SELECT`: подсчитывает количество строк, в которых столбец `t4` содержит значение `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="dccc5-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="dccc5-131">Эта инструкция должна вернуть значение `3`, так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="dccc5-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="dccc5-132">`INPUT__FILE__NAME LIKE '%.log'`: указывает Hive, что вернуть нужно только данные из файлов с расширением LOG.</span><span class="sxs-lookup"><span data-stu-id="dccc5-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="dccc5-133">Это предложение ограничивает поиск до файла sample.log, который содержит данные.</span><span class="sxs-lookup"><span data-stu-id="dccc5-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="dccc5-134">На панели инструментов выберите **Кластер HDInsight**, который вы хотите использовать для этого запроса.</span><span class="sxs-lookup"><span data-stu-id="dccc5-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="dccc5-135">Щелкните **Отправить**, чтобы выполнить инструкции как задание Hive.</span><span class="sxs-lookup"><span data-stu-id="dccc5-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Панель отправки](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="dccc5-137">Отобразится **сводка по заданию Hive** и информация о его выполнении.</span><span class="sxs-lookup"><span data-stu-id="dccc5-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="dccc5-138">Воспользуйтесь ссылкой **Обновить**, чтобы обновить информацию о задании. Обновляйте ее до тех пор, пока **состояние задания** не изменится на **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="dccc5-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![Сводка по завершенному заданию](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="dccc5-140">Воспользуйтесь ссылкой **Выходные данные задания** , чтобы просмотреть выходные данные этого задания.</span><span class="sxs-lookup"><span data-stu-id="dccc5-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="dccc5-141">Они содержат `[ERROR] 3`. Это значение, возвращенное данным запросом.</span><span class="sxs-lookup"><span data-stu-id="dccc5-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="dccc5-142">Запросы Hive можно также отправлять без создания проекта.</span><span class="sxs-lookup"><span data-stu-id="dccc5-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="dccc5-143">С помощью **обозревателя сервера** разверните узлы **Azure** > **HDInsight**, щелкните правой кнопкой мыши сервер HDInsight, а затем выберите **Написать запрос Hive**.</span><span class="sxs-lookup"><span data-stu-id="dccc5-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="dccc5-144">Отобразится документ **temp.hql** , в который нужно добавить следующие операторы HiveQL:</span><span class="sxs-lookup"><span data-stu-id="dccc5-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="dccc5-145">Эти операторы выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dccc5-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="dccc5-146">`CREATE TABLE IF NOT EXISTS`: создает таблицу, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="dccc5-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="dccc5-147">Так как не используется ключевое слово `EXTERNAL`, эта инструкция создает внутреннюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="dccc5-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="dccc5-148">Внутренние таблицы хранятся в хранилище данных Hive и управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="dccc5-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dccc5-149">В отличие от таблиц `EXTERNAL`, удаление внутренней таблицы приводит к удалению ее базовых данных.</span><span class="sxs-lookup"><span data-stu-id="dccc5-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="dccc5-150">`STORED AS ORC`: позволяет сохранить данные в формате ORC.</span><span class="sxs-lookup"><span data-stu-id="dccc5-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="dccc5-151">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="dccc5-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="dccc5-152">`INSERT OVERWRITE ... SELECT`: выбирает строки из таблицы `log4jLogs`, которые содержат `[ERROR]`, а затем вставляет эти данные в таблицу `errorLogs`.</span><span class="sxs-lookup"><span data-stu-id="dccc5-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="dccc5-153">На панели инструментов щелкните **Отправить** , чтобы выполнить задание.</span><span class="sxs-lookup"><span data-stu-id="dccc5-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="dccc5-154">Определить, было ли задание выполнено успешно, можно по значению в поле **Состояние задания** .</span><span class="sxs-lookup"><span data-stu-id="dccc5-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="dccc5-155">Убедитесь в том, что задание создало таблицу. Для этого в **обозревателе сервера** разверните **Azure** > **HDInsight** > ваш кластер HDInsight > **Базы данных Hive** > **По умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="dccc5-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="dccc5-156">Должны быть отображены таблицы **errorLogs** и **log4jLogs**.</span><span class="sxs-lookup"><span data-stu-id="dccc5-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="dccc5-157"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dccc5-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="dccc5-158">Как вы видите, средства HDInsight для Visual Studio упрощают работу с запросами Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dccc5-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="dccc5-159">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="dccc5-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="dccc5-160">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="dccc5-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="dccc5-161">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="dccc5-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="dccc5-162">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="dccc5-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="dccc5-163">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="dccc5-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="dccc5-164">Дополнительная информация об инструментах HDInsight для Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="dccc5-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="dccc5-165">Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive</span><span class="sxs-lookup"><span data-stu-id="dccc5-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
