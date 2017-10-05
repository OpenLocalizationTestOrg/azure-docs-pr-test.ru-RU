---
title: "Использование Hadoop Hive и удаленного рабочего стола в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как подключиться к кластеру HDInsight с помощью удаленного рабочего стола, а затем выполнить запросы Hive с помощью интерфейса командной строки Hive."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="256de-103">Использование Hive с Hadoop в HDInsight с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="256de-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="256de-104">В этой статье вы узнаете, как подключиться к кластеру HDInsight с помощью удаленного рабочего стола, а затем выполнить запросы Hive с помощью интерфейса командной строки Hive.</span><span class="sxs-lookup"><span data-stu-id="256de-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="256de-105">Удаленный рабочий стол доступен только в кластерах HDInsight под управлением операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="256de-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="256de-106">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="256de-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="256de-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="256de-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="256de-108">При использовании HDInsight 3.4 или более поздней версии см. сведения о выполнении запросов Hive непосредственно в кластере из командной строки: [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="256de-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="256de-109"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="256de-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="256de-110">Чтобы выполнить действия, описанные в этой статье, необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="256de-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="256de-111">Кластер HDInsight на платформе Windows (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="256de-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="256de-112">Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="256de-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="256de-113"><a id="connect"></a>Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="256de-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="256de-114">Запустите протокол удаленного рабочего стола для кластера HDInsight, а затем выполните подключение, следуя инструкциям раздела [Подключение к кластерам HDInsight с использованием RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="256de-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="256de-115"><a id="hive"></a>Использование команды Hive</span><span class="sxs-lookup"><span data-stu-id="256de-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="256de-116">После подключения к рабочему столу для кластера HDInsight сделайте следующее для работы с Hive:</span><span class="sxs-lookup"><span data-stu-id="256de-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="256de-117">На рабочем столе HDInsight запустите **командную строку Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="256de-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="256de-118">Введите следующую команду, чтобы запустить интерфейс командной строки Hive:</span><span class="sxs-lookup"><span data-stu-id="256de-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="256de-119">После запуска интерфейса командной строки появится командная строка Hive: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="256de-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="256de-120">С помощью этого интерфейса командной строки введите следующие операторы, чтобы создать таблицу с именем **log4jLogs** , используя пример данных:</span><span class="sxs-lookup"><span data-stu-id="256de-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="256de-121">Эти операторы выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="256de-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="256de-122">**DROP TABLE**: удаление таблицы и файла данных, если таблица уже существует.</span><span class="sxs-lookup"><span data-stu-id="256de-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="256de-123">**CREATE EXTERNAL TABLE**: создание новой "внешней" таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="256de-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="256de-124">Внешние таблицы хранят только определение самой таблицы в Hive, в то время как данные остаются в исходном расположении.</span><span class="sxs-lookup"><span data-stu-id="256de-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="256de-125">Внешние таблицы необходимо использовать в тех случаях, когда ожидается, что исходные данные будут обновляться внешним источником, таким как автоматизированный процесс передачи данных или другой операцией MapReduce, при этом нужно, чтобы запросы Hive использовали самые последние данные.</span><span class="sxs-lookup"><span data-stu-id="256de-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="256de-126">Удаление внешней таблицы **не** приводит к удалению данных, будет удалено только определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="256de-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="256de-127">**ROW FORMAT**: инструкции по форматированию данных для Hive.</span><span class="sxs-lookup"><span data-stu-id="256de-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="256de-128">В данном случае поля всех журналов разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="256de-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="256de-129">**STORED AS TEXTFILE LOCATION**: информация для Hive о расположении хранения данных (каталог example/data) и о их формате (текстовый).</span><span class="sxs-lookup"><span data-stu-id="256de-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="256de-130">**SELECT**: подсчитывает количество строк, в которых столбец **t4** содержит значение **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="256de-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="256de-131">Эта команда должна вернуть значение **3** , так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="256de-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="256de-132">**INPUT__FILE__NAME LIKE '%.log'** — указывает Hive, что вернуть нужно только данные из файлов с расширением LOG.</span><span class="sxs-lookup"><span data-stu-id="256de-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="256de-133">Это ограничивает поиск файлом sample.log, в котором содержатся данные, и предотвращает возврат данных из других примеров файлов данных, не соответствующих определенной нами схеме.</span><span class="sxs-lookup"><span data-stu-id="256de-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="256de-134">Используйте следующие операторы, чтобы создать новую "внутреннюю" таблицу с именем **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="256de-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="256de-135">Эти операторы выполняют следующие действия.</span><span class="sxs-lookup"><span data-stu-id="256de-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="256de-136">**CREATE TABLE IF NOT EXISTS**: создание таблицы, если она до этого не существовала.</span><span class="sxs-lookup"><span data-stu-id="256de-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="256de-137">Так как ключевое слово **EXTERNAL** не использовалось, такая таблица будет внутренней, то есть хранящейся в хранилище данных Hive и полностью управляемой Hive.</span><span class="sxs-lookup"><span data-stu-id="256de-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="256de-138">В отличие от **внешних** таблиц, удаление внутренней таблицы приводит к удалению базовых данных.</span><span class="sxs-lookup"><span data-stu-id="256de-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="256de-139">**STORED AS ORC**: хранение данных в формате ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="256de-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="256de-140">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="256de-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="256de-141">**INSERT OVERWRITE ... SELECT**: выбирает строки из таблицы **log4jLogs**, которые содержат значение **[ERROR]**, а затем вставляет данные в таблицу **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="256de-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="256de-142">Чтобы убедиться, что в таблице **errorLogs** сохранены только строки, столбец t4 которых содержит значение **[ERROR]**, воспользуйтесь следующим оператором, чтобы отобразить все строки из таблицы **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="256de-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="256de-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="256de-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="256de-144">В результате операции должны быть возвращены три строки, в которых столбец t4 содержит значение **[ERROR]** .</span><span class="sxs-lookup"><span data-stu-id="256de-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="256de-145"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="256de-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="256de-146">Как видите, с помощью команды Hive можно с легкостью выполнять интерактивные запросы Hive в кластере HDInsight, отслеживать состояние задания и получать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="256de-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="256de-147"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="256de-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="256de-148">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="256de-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="256de-149">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="256de-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="256de-150">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="256de-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="256de-151">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="256de-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="256de-152">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="256de-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="256de-153">Если вы используете Tez с Hive, обратитесь к следующим документам для сведений об отладке:</span><span class="sxs-lookup"><span data-stu-id="256de-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="256de-154">Использование пользовательского интерфейса Tez в HDInsight на платформе Windows</span><span class="sxs-lookup"><span data-stu-id="256de-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="256de-155">Использование представления Ambari Tez в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="256de-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
