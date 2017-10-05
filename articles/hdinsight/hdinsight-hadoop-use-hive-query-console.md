---
title: "Использование Hadoop Hive в консоли запросов в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как выполнять запросы Hive в кластере HDInsight Hadoop из браузера с помощью консоли запросов HDInsight для Интернета."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="2422a-103">Выполнение запросов Hive с помощью консоли запросов</span><span class="sxs-lookup"><span data-stu-id="2422a-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2422a-104">В этой статье вы узнаете, как выполнять запросы Hive в кластере HDInsight Hadoop из браузера с помощью консоли запросов HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2422a-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2422a-105">Консоль запросов HDInsight доступна только в кластерах HDInsight на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="2422a-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2422a-106">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2422a-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2422a-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2422a-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="2422a-108">При использовании HDInsight 3.4 или более поздней версии см. сведения о выполнении запросов Hive из браузера: [Использование представления Hive с Hadoop в HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="2422a-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="2422a-109"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2422a-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="2422a-110">Чтобы выполнить действия, описанные в этой статье, необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="2422a-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="2422a-111">Кластер HDInsight Hadoop на платформе Windows</span><span class="sxs-lookup"><span data-stu-id="2422a-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="2422a-112">Современный браузер</span><span class="sxs-lookup"><span data-stu-id="2422a-112">A modern web browser</span></span>

## <span data-ttu-id="2422a-113"><a id="run"></a> Выполнение запросов Hive с помощью консоли запросов</span><span class="sxs-lookup"><span data-stu-id="2422a-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="2422a-114">Откройте в браузере страницу с адресом **https://CLUSTERNAME.azurehdinsight.net**, где **CLUSTERNAME** — имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2422a-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="2422a-115">При появлении соответствующего запроса введите имя пользователя и пароль, использованные при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="2422a-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="2422a-116">Среди ссылок в верхней части страницы выберите **Редактор Hive**.</span><span class="sxs-lookup"><span data-stu-id="2422a-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="2422a-117">Откроется форма, которую можно использовать для ввода операторов HiveQL, которые будут выполняться в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2422a-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![Редактор Hive](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="2422a-119">Замените текст `Select * from hivesampletable` следующими операторами HiveQL:</span><span class="sxs-lookup"><span data-stu-id="2422a-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="2422a-120">Эти операторы выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2422a-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2422a-121">**DROP TABLE**: удаление таблицы и файла данных, если таблица уже существует.</span><span class="sxs-lookup"><span data-stu-id="2422a-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="2422a-122">**CREATE EXTERNAL TABLE**: создание новой «внешней» таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="2422a-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="2422a-123">Внешние таблицы хранят только описание самой таблицы в Hive, в то время как данные остаются в исходном расположении.</span><span class="sxs-lookup"><span data-stu-id="2422a-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2422a-124">Внешние таблицы необходимо использовать в тех случаях, когда ожидается, что исходные данные будут обновляться внешним источником, таким как автоматизированный процесс передачи данных или другой операцией MapReduce, при этом нужно, чтобы запросы Hive использовали самые последние данные.</span><span class="sxs-lookup"><span data-stu-id="2422a-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="2422a-125">Удаление внешней таблицы **не** приводит к удалению данных, будет удалено только определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="2422a-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="2422a-126">**ROW FORMAT**: инструкции по форматированию данных для Hive.</span><span class="sxs-lookup"><span data-stu-id="2422a-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="2422a-127">В данном случае поля всех журналов разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="2422a-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="2422a-128">**STORED AS TEXTFILE LOCATION**: информация для Hive о расположении хранения данных (каталог example/data) и об их формате (текстовый).</span><span class="sxs-lookup"><span data-stu-id="2422a-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="2422a-129">**SELECT**: подсчет количества строк, в которых столбец **t4** содержит значение **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="2422a-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="2422a-130">Эта команда должна вернуть значение **3** , так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="2422a-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="2422a-131">**INPUT__FILE__NAME LIKE '%.log'** — указывает Hive, что вернуть нужно только данные из файлов с расширением LOG.</span><span class="sxs-lookup"><span data-stu-id="2422a-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="2422a-132">Это ограничивает поиск файлом sample.log, в котором содержатся данные, и предотвращает возврат данных из других примеров файлов данных, не соответствующих определенной нами схеме.</span><span class="sxs-lookup"><span data-stu-id="2422a-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="2422a-133">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="2422a-133">Click **Submit**.</span></span> <span data-ttu-id="2422a-134">В поле **Сеанс задания** в нижней части страницы должна отображаться подробная информация о задании.</span><span class="sxs-lookup"><span data-stu-id="2422a-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="2422a-135">После изменения значения поля **Состояние** на **Завершено** выберите **Просмотреть подробности** для задания.</span><span class="sxs-lookup"><span data-stu-id="2422a-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="2422a-136">На странице сведений **выходные данные задания** будут содержать `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="2422a-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="2422a-137">Чтобы скачать файл, содержащий выходные данные задания, можно нажать кнопку **Скачать** под этим полем.</span><span class="sxs-lookup"><span data-stu-id="2422a-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="2422a-138"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="2422a-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="2422a-139">Как можно видеть, консоль запросов позволяет с легкостью выполнять запросы Hive в кластере HDInsight, отслеживать состояние задания и получать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2422a-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="2422a-140">Чтобы получить дополнительную информацию об использовании консоли запросов Hive, выберите **Приступая к работе** в верхней части консоли запросов, а затем воспользуйтесь предоставленными примерами.</span><span class="sxs-lookup"><span data-stu-id="2422a-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="2422a-141">Каждый пример содержит пошаговые инструкции по анализу данных с помощью Hive, в том числе пояснения к операторами HiveQL, используемым в примере.</span><span class="sxs-lookup"><span data-stu-id="2422a-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="2422a-142"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2422a-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="2422a-143">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2422a-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="2422a-144">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2422a-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2422a-145">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2422a-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2422a-146">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2422a-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2422a-147">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2422a-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="2422a-148">Если вы используете Tez с Hive, обратитесь к следующим документам для сведений об отладке:</span><span class="sxs-lookup"><span data-stu-id="2422a-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="2422a-149">Использование пользовательского интерфейса Tez в HDInsight на платформе Windows</span><span class="sxs-lookup"><span data-stu-id="2422a-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="2422a-150">Использование представления Ambari Tez в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2422a-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
